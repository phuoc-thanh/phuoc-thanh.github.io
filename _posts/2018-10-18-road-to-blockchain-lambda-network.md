---
layout: post
title: "Lambda Chain: Network"
comments: true
description: "Road to Blockchain: Network"
keywords: "blockchain, proofofstake, proofofwork, bitcoin, haskell, lambda, p2p network, tcp connect"
---

Kỹ thuật xây dựng mạng ngang hàng ko hề mới mẻ, nhất là đối với kỹ sư thường xuyên làm việc với hạ tầng ở mức thấp như tcp-network, socket. Nếu xưa giờ bạn chỉ làm web, chỉ biết sử dụng http/POST/GET/json.. thì cũng ko sao, đây là cơ hội tốt để bạn đào sâu thêm về nền tảng bên dưới "web".

p2p-network thường là một mạng lưới máy tính (Node) sử dụng giao thức tcp để thông tin liên lạc qua lại lẫn nhau, trong trường hợp của blockchain, đó là những thông tin về transation, block, wallet..

Để xây dựng mạng p2p hoàn chỉnh, tôi cần 3 sub-module:

1. Connection: bao gồm các chức năng kết nối cơ bản trên nền tcp: khởi tạo kết nối peer-to-peer, sử dụng socket để gửi/nhận thông tin (message), lắng nghe/tiếp nhận/loại bỏ connections trên socket.

2. Message: Đóng vai trò là Parser, chuyên phân giải dữ liệu thô từ socket thành dạng dữ liệu có cấu trúc hoặc các câu lệnh để cho Node xử lý.

3. Node: Xử lý logic như tiếp nhận data/request từ peers (các node khác), broadcast thông tin lên network, mining coin, thêm/xoá dữ liệu trong memory pool, cập nhật blockchain, kí tên giao dịch bằng chữ kí số..

## Connection

Khởi tạo một node - có nghĩa là khởi tạo một tcp-server, bạn cần lấy ra một port nào đó trên máy, sau đó bind một socket cứng trên port đó, chuyên dùng để lắng nghe incoming requests từ các node khác. Việc này ko khó, hãy stack-overflow đi nào, nếu là Haskell, code sẽ tương tự như sau:

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

Và một function `listen_` để accept incoming requests vào "bound socket" trên. Nếu có yêu cầu kết nối từ địa chỉ mới, says hi rồi mở một socket mới cho địa chỉ đó. Thêm socket này vào peer list của Node server, rồi quay lại lắng nghe tiếp. Nó chính là một vòng lặp vô tận.

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

MVar [Socket] ở đây chính là peers list, lưu một loạt socket mà server đang kết nối đến.

Okay, vậy là tôi đã setup được một Tcp Server luôn luôn lắng nghe, luôn luôn thấu hiểu rồi, mà vẫn thấy thiếu thiếu cái gì nhỉ? Ahh, ko lẽ cứ bị động ngồi chờ, phải có một phương thức để chủ động kết nối nữa mới xong!

Function `connect_` cho phép chương trình kết nối vào những máy tính khác dựa vào thông số host, port. Nó cũng trả về kiểu socket nếu kết nối thành công.

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

Và kết nối được rồi thì sao nữa? Tất nhiên là phải giao tiếp rồi hehe, chúng ta cần gửi - và nhận message từ socket:

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

Sau khi đã có toàn bộ những function cơ bản cho hạ tầng tcp server, giờ chúng ta bắt đầu xây dựng Node, như đã nói ở trên, Node cần lưu data về transactions, blocks và peers trong bộ nhớ. Transaction thực là một dạng data cần lưu trữ đối với giao dịch tiền (kĩ thuật số), nhưng bạn có thể thử data khác nếu ko có ý định triển khai cryptocurrency.

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

Sau khi Node đã live, có khả năng lắng nghe và giao tiếp với node khác trong mạng, kế tiếp ta cần viết function để Node có thể handle liên tục những request tới, ví dụ như thêm xoá transaction, update block, mining...

Connection handle sẽ là vòng lặp, cứ mỗi 2 giây sẽ check bộ nhớ và lấy ra danh sách các peers (dạng Socket list), và từ mỗi Socket sẽ cố gắng đọc tin nhắn gửi đến.

```haskell
-- | Handle Connections
conn_handle :: NodeState -> IO ()
conn_handle st = do
    threadDelay 2000000
    conn <- tryReadMVar (_peers st)
    forM_ (fromJust conn) $ \s -> req_handle s st
    conn_handle st
```

## Message Parser

Sẽ có một parser để phân giải những tin nhắn nhận được từ socket ra thành structure data, specified command, Node sẽ dựa trên Command đó để call những function khác.

Kiểu data của Msg, nhận bytestring thô từ socket như "block:blockdata1234hashed" thì sẽ parse ra thành:

- Đây là lệnh thêm một block mới,
- Chuyển dữ liệu phía sau dấu ":" thành một cấu trúc block

```haskell
rawToMsg :: ByteString -> Msg
rawToMsg m = case (takeWhile (/=':') m) of
    "block" -> BlockReq (read data_ :: Block)
    "_id"   -> BlockIdx (read data_ :: Int)
    "txn"   -> TxnReq   (read data_ :: Transaction)
    msg     -> Raw msg
    where data_ = unpack . tail $ dropWhile (/=':') m
```

Và Node sẽ xử lý các dữ liệu này, vd như thêm transaction vào memory pool, update block mới.

```haskell
-- | Hanle incoming requests    
req_handle :: Socket -> NodeState -> IO ()    
req_handle sock st = do
    raw <- recv sock 1024
    unless (null raw) $ do
        case (rawToMsg raw) of          
            TxnReq txn -> modifyMVarMasked_ (_pool st) $ \txns -> return $ expand_pool txn txns
            BlockReq b -> modifyMVarMasked_ (_chain st) $ \lst -> return $ b:lst
            Raw m      -> print m

-- | Message Type: Raw, Request , Response
data Msg = Raw ByteString | BlockReq Block | BlockIdx Int | TxnReq Transaction
```

# End network part

Vậy là bạn đã setup xong một mạng p2p-network căn bản rồi đó. Congratulation.