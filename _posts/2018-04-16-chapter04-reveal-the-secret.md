---
layout: post
title: "Chapter 04: Reveal the Secret"
comments: true
description: "Nghệ thuật hắc ám - Phần 04: Giải mã bí mật"
keywords: "haskell, pure, functional, hijack, game, server, wireshark, tcp, packet, filter, network, injector, serialize"
---

Trong phần trước tôi có nói rằng tôi có chút kinh nghiệm với Network, ah ha, nhưng chỉ với Java thôi, còn với Haskell, lúc này tôi hoàn toàn ko biết một chút gì về Haskell Networking.

Từ những dữ liệu mà Wireshark mang lại cộng thêm những phân tích đầu tiên, lúc này tôi cần làm 2 việc:

- Giả lập những request chứng thực username/password tới HTTP Server

- Nhận response từ Http Server và tiếp tục giả lập TCP request tới TCP Server.

Nhưng tôi chưa bao giờ lập trình network với Haskell cả, khó!

---

# Request đến Http Server

Sau vài hôm tìm hiểu library và thực hành, tôi đã thành công trong việc gửi request tới Http Server. Http thì khá là suôn sẻ khi tôi chỉ cần gửi đúng những request như trong Wireshark bắt được và nhận được response là đã thành công rồi.

Đầu tiên là checkUser request (packet số 19 trong phần trước)

```haskell
import Data.ByteString.Lazy (ByteString)
import qualified Data.ByteString.Char8 as S
import qualified Data.ByteString.Lazy.Char8 as C

import Parser
import Network.HTTP.Simple

checkUserURI = "/payclient.ashx?op=CheckUser"

checkUserRq :: ByteString -> ByteString -> S.ByteString -> Request
checkUserRq u p h = setRequestPath checkUserURI -- u p h mean username, password, host
                  $ setRequestHost h
                  $ setRequestBodyLBS (userRqBody u p)
                  $ setRequestMethod "POST" defaultRequest

userRqBody :: ByteString -> ByteString -> ByteString
userRqBody u p   = C.append "partnerId=0&userName="
                 $ C.append u 
                 $ C.append "&deviceId=d80f998b16396187&serverMode=UNKNOWN&password="
                 $ C.append p "&refcode=0&gameId=46"
```

Tôi nhái lại y chang request thu được từ wireshark.

Tiếp theo là login verify request (packet số 55 trong phần trước)

```haskell     
loginVerify :: String -> String -> IO Player
loginVerify u p = do
    cf <- getConfig
    cResponse <- httpLBS $ checkUserRq (C.pack u) (C.pack p) (S.pack $ payHost cf)
    response <- httpLBS $ loginVerifyRq (getResponseBody cResponse)
                                        (S.pack $ apiHost cf) 
                                        (S.pack $ loginPath cf)
    return $ fromJust $ getUserData $ getResponseBody response

loginVerifyRq s host path = setRequestHost host
                          $ setRequestPath path
                          $ setRequestBodyLBS (loginRqBody s)
                          $ setRequestMethod "POST"
                          $ setRequestHeader "Content-Type" ["application/x-www-form-urlencoded"] defaultRequest    

loginRqBody :: ByteString -> ByteString
loginRqBody s = C.append "uid=" . C.append userId . C.append "&token=" $ C.append session "&os=and&version=75896"
    where session = C.drop 8 $ (!!) (C.split '&' s) 3
          userId  = C.drop 7 $ (!!) (C.split '&' s) 2

getUserData :: FromJSON a => ByteString -> Maybe a
getUserData s = decode $ C.append (C.drop 9 $ head $ C.split '}' s) ",\"chNumber\" : \"unknow\",\"amount\" : 0}"         
```

2 đoạn code trên ở 1 module tôi đặt tên là `HttpRq.hs`

Player mà các bạn thấy, là một kiểu dữ liệu có thể lưu được, tôi define Player trong module `Parser.hs`:

```haskell
data Player = Player { acc           :: String,
                       uid           :: String,
                       opname        :: String,
                       defaultsid    :: String,
                       displayNovice :: Integer,
                       create_time   :: Integer,
                       key           :: String,
                       chNumber      :: String,
                       amount        :: Integer }
                   deriving (Show, Eq, Generic)
```
Các thông tin cần thiết để thiết lập nên Player có thể get từ Http Server của Game, duy chỉ có chNumber và amount là không có, tôi sẽ nói chi tiết 2 mục này ở phần sau

---

# Request đến Tcp Server

Okay tôi đã gửi Http Request và nhận Response đúng như mong đợi. Công việc tiếp theo là Inject những gói data vào TCP Server, đây mới chính là Game Server của Game X.

Ở đây phải nói thêm là sau vài ngày mày mò tìm hiểu, tôi phát hiện 1 lỗi rất lớn của Game X. Thông thường Tcp Request sẽ nhận các thông số từ Http Response như uid, key, default_server, create_time... rồi dùng những thông số này để tạo request gửi tới Tcp Server.

Lỗi ở chỗ, Tcp server không kiểm tra tính hợp lệ của những thông số này, tôi có thể gửi 1 Http request tới Http Server, nhận được key/time trả về trong Http Response. Sau đó tôi có thể dùng cặp thông tin key/time này để gửi đến TCP Server trong mọi hoàn cảnh sau đó. Nghĩa là bạn chỉ cần đăng nhập 1 lần duy nhất, sau đó có thể chơi game mà không cần log-in! Crazy?

Yes, chính xác là như vậy, Game X đã bỏ qua một lỗi sơ đẳng nhưng cực kỳ nghiêm trọng. Hiện tại tôi chưa thấy được lợi ích, nhưng càng về sau, chiến tranh nổ ra thì cái lỗi củ chuối này sẽ là đòn chí mạng!

Lúc này, đa số thông tin lấy đc từ Http Response, đã đầy đủ. Tôi tiếp tục tìm hiểu tới Tcp Server.

Ban đầu tôi dùng Tcp Streams, thư viện tích hợp sẵn việc gửi nhận gói tcp và đưa dữ liệu vào Streams, nhưng sau đó tôi lại chuyển qua dùng gói Network cơ bản của Haskell để tự tạo nên Injector. Tính tôi thích mọi thứ thật đơn giản, chỉ những thứ thiết yếu :)

Đây là module Injector, thuở sơ khai.

```haskell
module Injector where

import HttpRq

import Network.Socket hiding (send, recv)
import Network.Socket.ByteString (send, recv, sendAll)

connect_ :: HostName -> ServiceName -> IO Socket
connect_ host port = do 
    addrinfos <- getAddrInfo Nothing (Just host) (Just port)
    let serveraddr = head addrinfos
    sock <- socket (addrFamily serveraddr) Stream defaultProtocol
    connect sock (addrAddress serveraddr)
    return sock

login :: String -> String -> IO Player
login u p = do res <- loginVerify u p
               uServer <- getServerInfo (defaultsid res)
               sock <- connect_ (ip uServer) (port uServer)
               sendAll sock $ loginData res (C.pack $ defaultsid res)
               msg <- recv sock 256
               close sock
               return $ Player u (uid res) (opname res) (defaultsid res)
                               (displayNovice res) (create_time res) (key res) 
                               (show . getChNumber $ encode msg)
                               (amount res)
```

Tất nhiên, để test thì tôi vẫn phải copy phần loginData mà Wireshark bắt được, inject vào đúng ip:port của server. Phần build data packet sẽ tiếp tục ngay sau đây. :))

---

# Phân tích từng Byte dữ liệu

Đối với Tcp data, những ltv tạo ra game sẽ phải serialize/deserialize data sao cho dữ liệu gửi đi thật tiết kiệm, thật nhỏ nhưng phải đảm bảo toàn vẹn. Có thể bạn ko biết, những mỗi giây, TCP Server sẽ xử lý rất nhiều request, con số có thể lên đến hàng trăm, hàng ngàn, và thậm chí nhiều hơn thế. Đây là tôi đang nói trong phạm vi 1 Game Server.

Mỗi data packet gửi đi/về tôi thu được trong Wireshark, tôi đều mày mò so sánh, giải mã. Chiến dịch giải mã từng byte trong gói data giao tiếp giữa Client-Server đã tiêu tốn của tôi rất nhiều đêm mất ngủ.

Sau rất nhiều nỗ lực phân tích, tìm kiếm, kiểm thử. Tôi cuối cùng đã giải mã được cấu trúc dữ liệu giao tiếp giữa Client-Server của Game X. Các bạn hãy lưu ý rằng đây chính là bước quan trọng nhất và cũng là khó nhất của công việc hack game online: Encode and Decode Packet Structure!

Kết quả tôi đính kèm theo trong file `Serializer.hs` sau đây, tôi có note lại cấu trúc dữ liệu mà Game X đã sử dụng trong phần comment.

```haskell

module Serializer where

import qualified Data.ByteString.Char8 as C
import Data.ByteString.Base16
import Data.List.Split
import Numeric


-- Packet structure
-- packet info = 2 bytes (1 byte info + 1 flag byte) represents the length of packet
-- index info  = 2 bytes (1 index byte + 1 byte: ff) represents the index of this packet in the streams
-- data info   = 2 bytes (1 byte info + 1 flag byte) represents the length of data
-- data        = x bytes (x-1 byte data + 1 flag byte) contains the data

decToHex :: (Show a, Integral a) => a -> C.ByteString
decToHex c
    | c < 16 = C.append "0" . C.pack $ showHex c ""
    | otherwise = C.pack $ showHex c ""

hexSerialize :: (Show a, Integral a) => a -> C.ByteString
hexSerialize d = fst . decode $ C.append (decToHex (d + 4))
                              $ C.append "0003ff"
                              $ C.append (decToHex d) "00"

hexLoginSerialize :: (Show a, Integral a) => a -> C.ByteString                           
hexLoginSerialize d = fst . decode $ C.append (decToHex (d + 4))
                                   $ C.append "0001ff"
                                   $ C.append (decToHex d) "00"

hexEnterSerialize :: (Show a, Integral a) => a -> C.ByteString                             
hexEnterSerialize d = fst . decode $ C.append (decToHex (d + 4))
                                   $ C.append "0002ff"
```

Ở đây tôi phải viết 3 functions serialize, vì các gói dữ liệu được đánh số thứ tự riêng rẽ, login có flag byte khác với enter, login và enter có flag byte khác với các gói dữ liệu thông thường khác... (0001ff, 0002ff, 0003ff)

Mặt khác, dữ liệu được encode ở dạng Base16 String, nó sẽ hiển thị toàn số Hex, bạn cần dùng Wireshark để xem xét từng byte. Rất may mắn, Haskell có package ByteString.Base16 giúp tôi giải quyết chuyện này. Công việc của Serializer là từ những dữ liệu con người có thể đọc hiểu (String), build ra một gói Data phù hợp, có thể dùng để gửi tới Game Server (Hex bytes).

---

# Chuỗi Byte bị đảo ngược

Ở function login của Injector, sau khi gửi thành công gói login data tới TCP Server, Client sẽ nhận được thông tin Character ID. Character ID là 1 dạng mã định danh cho nhân vật, tương tự như cột Id chúng ta hay dùng trong SQL Database.

Để get được số ID này, tôi lấy toàn bộ dữ liệu từ socket (nhận đc từ Tcp Server) và phân tích tiếp.

Lần này đội dev Game X không chỉ đơn giản mã hóa Base16, mà reverse luôn order của các bytes dữ liệu theo từng cặp, tăng mức độ khó của việc bẻ khóa.

Tôi thêm 1 function vào Serializer chuyên xử lý mấy tình yêu này:

```haskell
hexDeserialize :: C.ByteString -> Integer
hexDeserialize "" = 0
hexDeserialize b  = read . concat . ("0x":) . reverse . chunksOf 2 $ C.unpack b
```

Và trong Injector, tôi get 256 bytes từ socket, sau đó gọi 1 function tên là getChNumber để lấy đc Character ID từ 256 bytes này.

Cắt, dán đúng những bytes chứa CharacterID, sau đó deserialize:

```haskell
getChNumber :: ByteString -> Integer
getChNumber = hexDeserialize . C.take 8 . C.drop 14
```
---

# Tích hợp mọi thứ

Sau khi xây dựng đủ các module cần thiết, chuyện tích hợp khác đơn giản, lúc này tôi có:

***HttpRq.hs:*** có nhiệm vụ fake Http request để gửi tới Http Server.

***Injector.hs:*** có nhiệm vụ fake Tcp request để gửi tới Tcp Server.

***Serializer.hs:*** Encode/decode byte data.

***Authenticator.hs:*** Nhận thông tin từ HttpRq và build Player data, build login packet cho Injector.

***Parser.hs*** Data model cho Player, Server, bao gồm cả lưu/đọc file json.

***Player.json:*** Nơi lưu trữ thông tin player, có thể xem như một database.


