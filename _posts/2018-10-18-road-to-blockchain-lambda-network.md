---
layout: post
title: "Lambda-Chain Network"
comments: true
description: "Road to Blockchain - Lambda-chain Network"
keywords: "blockchain, proofofstake, proofofwork, bitcoin, haskell, lambada"
---

Kỹ thuật xây dựng mạng ngang hàng ko hề mới mẻ, nhất là đối với kỹ sư thường xuyên làm việc với hạ tầng ở mức thấp như tcp-network, socket. Nếu xưa giờ bạn chỉ làm web, chỉ biết sử dụng http/POST/GET/json.. thì cũng ko sao, đây là cơ hội tốt để bạn đào sâu thêm về nền tảng bên dưới "web".

p2p-network thường là một mạng lưới máy tính (Node) sử dụng giao thức tcp để thông tin liên lạc qua lại lẫn nhau, thông báo cho các node khác biết về transation, block mới, cập nhật và động bộ với nhau.

## Connection

Http request, đều được khởi tạo từ tcp, và đặc biệt dành cho việc hiển thị web. Nhưng ko phải vai trò của tcp chỉ là vậy, nó còn được sử dụng rất nhiều, và nếu hiểu giao thức tcp, việc sử dụng nó đơn giản và nhẹ nhàng hơn http/json rất nhiều.

Khởi tạo một node, bạn cần kiếm một địa chỉ port nào đó để bind một socket cứng trên port đó, chuyên dùng để lắng nghe incoming requests từ các node khác. Việc này ko khó, hãy stack-overflow đi nào, nếu là Haskell, code sẽ tương tự như sau:

```haskell
-- | Listen on a bound socket
listenOn :: PortNumber -> IO Socket
listenOn p2p_port = do
    sock <- socket AF_INET Stream 0                -- create socket
    setSocketOption sock ReuseAddr 1               -- make socket immediately reusable - eases debugging.
    bind sock (SockAddrInet p2p_port iNADDR_ANY)   -- listen on TCP p2p_port as config.
    listen sock 32                                 -- set a max of 32 queued connections
    print $ "Lambda-client is now listening on port: " ++ (show p2p_port)
    threadDelay 4096
    return sock
```

Và một function khác để accept incoming requests vào `bound socket` trên,

```haskell
-- | Listen n Accept incoming connections
listen_ :: Socket -> MVar [Socket] -> IO ()
listen_ sock socks = do
    conn   <- accept sock
    print  $ "A new connection is established. Sock_addr: " ++ (show $ snd conn)
    -- send welcome msg, then modify list of peers (MVar peers)
    sendAll (fst conn) $ append "You are connected to: " (pack $ show sock)
    modifyMVarMasked_ socks $ \lst -> return $ (fst conn):lst
    listen_ sock socks
```

MVar [Socket] ở đây là một bộ nhớ của Node để lưu toàn bộ những connection đến Node, có thể gọi là peers, ngoài ra node cũng cần phải lưu cả transaction pool và blockchain:


Okay, vậy là tôi đã setup được một Node với bound socket của nó chuyên lắng nghe và accept connections, vậy thiếu thiếu cái gì nhỉ. Ahh, ko lẽ cứ bị động ngồi chờ, phải có một phương thức để chủ động kết nối nữa mới xong!

```haskell
-- | Connect with default settings of Network.Socket
connect_ :: (HostName, ServiceName) -> IO Socket
connect_ (host, port) = do 
    addrinfos <- getAddrInfo Nothing (Just host) (Just port)
    let serveraddr = head addrinfos
    sock <- socket (addrFamily serveraddr) Stream defaultProtocol
    connect sock (addrAddress serveraddr)
    threadDelay 1024
    msg <- recv sock 256 -- receive welcome msg
    print msg
    return sock
```


Và kết nối được rồi thì sao nữa? Tất nhiên kết nối được rồi thì phải giao tiếp, tcp gửi - và nhận message từ socket, stackoverflow tiếp chứ ^___^

```haskell
-- | Send a message on specified socket, then try receive 1024 bytes of response
sendReq :: Socket -> ByteString -> IO ()
sendReq sock msg = do
    -- this is because of windows 7 ghci put "\r" character to end the string
    -- let msg = C.init raw
    sendAll sock msg
    threadDelay 2048
    res <- recv sock 1024
    print res

-- | Send a message to whole network (peers)    
sendNetwork :: [Socket] -> ByteString -> IO ()
sendNetwork socks msg = do
    forM_ socks $ \sock -> sendAll sock msg    
```

## Go live a node

Sau khi đã có toàn bộ những function cơ bản cho hạ tầng tcp, giờ chúng ta bắt đầu xây dựng Node, như đã nói ở trên, Node cần lưu data về transactions, blocks và peers trong bộ nhớ.


```haskell
data NodeState = NodeState {
    _chain :: MVar [Block],
    _pool  :: MVar [Transaction],
    _peers :: MVar [Socket]
}
```

Rồi ta có thể go live một node trên port (được nhập vào), trả ra một node_state - rỗng.

```haskell
-- | Go live a node, with empty chain, peers and txn_pool
import Network.Connection

go_live p2p_port = do
    db         <- start_lmdb
    sock       <- listenOn p2p_port
    blockchain <- newEmptyMVar
    txn_pool   <- newMVar mempty
    peers      <- newMVar mempty
    -- Initiate Node State
    let state  = NodeState {
        _chain = blockchain,
        _pool  = txn_pool,
        _peers = peers
    }
    forkIO $ listen_ sock (_peers state)
    forkIO $ conn_handle state
    return state
```

## Functional

Sau khi Node đã live, có khả năng lắng nghe và giao tiếp với node khác trong mạng, kế tiếp ta cần viết function để Node có thể handle liên tục những request tới, ví dụ như thêm xoá transaction, mining...

```haskell
-- | Handle Connections
conn_handle :: NodeState -> IO ()
conn_handle st = do
    threadDelay 2000000
    conn <- tryReadMVar (_peers st)
    forM_ (fromJust conn) $ \s -> req_handle s st
    conn_handle st

-- | Hanle incoming requests    
req_handle :: Socket -> NodeState -> IO ()    
req_handle sock st = do
    raw <- recv sock 1024
    unless (null raw) $ do
        case (rawToMsg raw) of          
            TxnReq txn -> modifyMVarMasked_ (_pool st) $ \txns -> return $ expand_pool txn txns
            BlockReq b -> modifyMVarMasked_ (_chain st) $ \lst -> return $ b:lst
            Raw m      -> print m
```

Kiểu data của Msg:

```haskell
-- | Message Type: Raw, Request , Response
data Msg = Raw ByteString | BlockReq Block | BlockIdx Int | TxnReq Transaction

rawToMsg :: ByteString -> Msg
rawToMsg m = case (takeWhile (/=':') m) of
    "block" -> BlockReq (read data_ :: Block)
    "_id"   -> BlockIdx (read data_ :: Int)
    "txn"   -> TxnReq   (read data_ :: Transaction)
    msg     -> Raw msg
    where data_ = unpack . tail $ dropWhile (/=':') m
```