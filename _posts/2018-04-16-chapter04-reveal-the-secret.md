---
layout: post
title: "Chapter 04: Reveal the Secret"
comments: true
description: "Nghệ thuật hắc ám - Phần 04: Giải mã bí mật"
keywords: "haskell, pure, functional, hijack, game, server, wireshark, tcp, packet, filter, network, injector"
---

# Những dòng code đầu tiên

Trong phần trước tôi có nói rằng tôi có chút kinh nghiệm với Network, ah ha, nhưng chỉ với Java thôi, còn với Haskell, lúc này tôi hoàn toàn ko biết một chút gì về Haskell Networking.

Từ những dữ liệu mà Wireshark mang lại công thêm những phân tích đầu tiên, lúc này tôi cần làm 2 việc:

- Giả lập những request chứng thực username/password tới HTTP Server

- Nhận response từ Http Server và tiếp tục giả lập TCP request tới TCP Server.

Nhưng tôi chưa bao giờ lập trình network với Haskell cả, khó!

Sau vài hôm tìm hiểu library và thực hành, tôi đã thành công trong việc gửi request tới Http Server. Http thì khá là suôn sẻ khi tôi chỉ cần gửi đúng những request như trong Wireshark bắt được và nhận được response là đã thành công rồi.

Đầu tiên là checkUser request:

```haskell
import Data.ByteString.Lazy (ByteString)
import qualified Data.ByteString.Char8 as S
import qualified Data.ByteString.Lazy.Char8 as C

import Parser
import Network.HTTP.Simple

checkUserURI = "/payclient.ashx?op=CheckUser"

checkUserRq :: ByteString -> ByteString -> S.ByteString -> Request
checkUserRq u p h = setRequestPath checkUserURI -- u p h mean username, passwork, host
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

Tiếp theo là login verify request (request số 55 trong phần trước)

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

Player mà các bạn thấy chính là một kiểu dữ liệu có thể lưu được, tôi define Player trong module `Parser.hs`:

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

# Chướng ngại vật đầu tiên: giải mã dữ liệu TCP

Okay tôi đã gửi Http Request và nhận Response đúng như mong đợi. Công việc tiếp theo là Inject những gói data vào TCP Server, đây mới chính là Game Server của Game X.

Ở đây phải nói thêm là sau vài ngày mày mò tìm hiểu, tôi phát hiện 1 lỗi rất lớn của Game X. Thông thường Tcp Request sẽ nhận các thông số từ Http Response như uid, key, default server, create time... rồi dùng những thông số này để tạo request gửi tới Tcp Server.

Lỗi ở chỗ, Tcp server không kiểm tra tính hợp lệ của những thông số này, tôi có thể gửi 1 Http request tới Http Server, nhận được time, key trả về trong Http Response. Sau đó tôi có thể dùng cặp thông tin key/time này để gửi đến TCP Server trong mọi hoàn cảnh sau đó. Nghĩa là bạn chỉ cần đăng nhập 1 lần duy nhất, sau đó có thể chơi game mà không cần log-in! Crazy?

Yes, chính xác là như vậy, Game X đã bỏ qua một lỗi sơ đẳng nhưng cực kỳ nghiêm trọng. Hiện tại tôi chưa thấy được lợi ích, nhưng càng về sau, chiến tranh nổ ra thì cái lỗi củ chuối này sẽ là đòn chí mạng!

Lúc này, đa số thông tin lấy đc từ Http Response, đã đầy đủ. Tôi tiếp tục tìm hiểu tới Tcp Server.

Đối với tcp data, những ltv tạo ra game sẽ phải serialize/deserialize data sao cho dữ liệu gửi đi thật tiết kiệm, thật nhỏ nhưng phải đảm bảo toàn vẹn. Có thể bạn ko biết, những mỗi giây, TCP Server sẽ xử lý rất nhiều request, con số có thể lên đến hàng trăm, hàng ngàn, và thậm chí nhiều hơn thế. Đây là tôi đang nói trong phạm vi 1 Game Server.

---

# Phân tích từng Byte dữ liệu

Mỗi gói packet gửi đi/về tôi thu được trong Wireshark, tôi đều mày mò so sánh, giải mã. Đây chính là giai đoạn khó khăn và thử thách nhất trong toàn bộ quá trình tôi hack game này.

Chiến dịch giải mã từng byte trong gói data giao tiếp giữa Client-Server đã tiêu tốn của tôi rất nhiều đêm mất ngủ.

Sau rất nhiều nỗ lực phân tích, tìm kiếm, kiểm thử. Tôi cuối cùng đã giải mã được cấu trúc dữ liệu giao tiếp giữa Client-Server của Game X. Các bạn hãy lưu ý rằng đây chính là bước quan trọng nhất và cũng là khó nhất của công việc hack game: Encode and Decode Packet Structure!

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

hexDeserialize :: C.ByteString -> Integer
hexDeserialize "" = 0
hexDeserialize b  = read . concat . ("0x":) . reverse . chunksOf 2 $ C.unpack b

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

Ở đây tôi phải viết 3 functions serialize, vì các gói dữ liệu được đánh số thứ tự riêng rẽ, login có flag byte khác với enter, login và enter có flag byte khác với các gói dữ liệu thông thường khác...

Flag byte là "00" nhé :)

Mặt khác, dữ liệu được encode ở dạng Base16 String, nó sẽ hiển thị toàn số Hex, bạn cần dùng Wireshark để xem xét từng byte. Rất may mắn, Haskell có package ByteString.Base16 giúp tôi giải quyết chuyện này. Công việc của tôi là tạo ra một Module dịch thuật, tạo ra Network Package to send từ những dữ liệu con người có thể đọc hiểu.

---

# Minh chứng đầu tiên

Sau khi tôi giải mã và viết xong được module tạo Tcp Packet, cái cần thiết bây giờ là 1 Tcp Injector để tiêm những gói này vào Game Server.

Ban đầu tôi dùng Tcp Streams, thư viện tích hợp sẵn việc gửi nhận gói tcp và đưa dữ liệu vào Streams, nhưng sau đó tôi lại dùng gói Network cơ bản của Haskell để tự tạo nên Injector. Tính tôi thích mọi thứ thật đơn giản, chỉ những thứ thiết yếu :)

Bấy giờ, mục tiêu của tôi chỉ là login vào được game. Nếu tôi đang mở Game X bằng điện thoại (or Nox), mà chạy được Injector đá tôi ra khỏi game là đã thành công (Game X có cơ chế người login sau đá người login trước).

Đây là module login của tôi, thuở sơ khai.

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

Và Module `Authenticator.hs`, nơi tôi giả lập lại những Packet login vào game (Giả lại gói đăng nhập từ TCP packet tôi bắt đc ở phần trước)

* getServerInfo là lấy ip và port từ server, các bạn có thể xem chi tiêt trong github.

* loginData là User Data được function build ra tcp data từ những dữ liệu chứng thực, các bạn có thể xem chi tiết trên Gibhub

---

# Một bước tiến dài

Khi tôi dùng Injector login vào được game và đá acc của tôi ra trên điện thoại, tôi có cảm giác như đã chiến thắng chính bản thân mình.

Từ đây, tôi biết Game X đã nằm trong tầm tay...


