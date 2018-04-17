---
layout: post
title: "Chapter 05: The Art of Stealing"
comments: true
description: "Nghệ thuật hắc ám - Phần 05: Nghệ thuật kiếm chác"
keywords: "haskell, pure, functional, hijack, game, server, wireshark, tcp, packet, filter, network, injector"
---

# Cá cược online và Threading

Tôi tận dùng ngày thứ 7 free để code nốt tính năng cược Xu. Lần này nhiệm vụ khá dễ dàng, vẫn cách cũ là fake lại request từ Wireshark.

Test Ok, nhưng chưa dùng được ngay, vào kỳ liên chiến tuần sau đó thì tình yêu của tôi mới chính thức lên sóng...

Ko có gì khó, tôi mở tạo 1 file War.hs chuyên dùng cược xu:

```haskell
main :: IO ()
main = do 
    winBet
    threadDelay 3600000
    loseBet

-- the last 1000 xu should bet 10 times 100xu
bet :: Integer -> Socket -> ByteString -> IO ()
bet 0 c idx = close c
bet 1 c idx = sendNTimes 10 c (bet100 idx)
bet n c idx = do sendAll c (betX idx)
                 bet (n - 1) c idx

-- bet 3 match same time
quickBet :: Player -> [ByteString] -> IO ()                  
quickBet p codes = do
    conn <- joinWorld p
    forM_ codes $ \c -> forkIO $ do
        bet (amount p) conn c

winBet :: IO ()
winBet = do
    pls <- players -- players whom bet the win side
    forM_ pls $ \p -> forkIO $ quickBet p winC
                  
loseBet :: IO ()
loseBet = do 
    pls <- buffPls -- players whom bet the lose side
    forM_ pls $ \p -> forkIO $ quickBet p loseC                 

winC = ["28001474"] -- the id of win player
loseC = ["28001474"] -- the id of lose player
```

Đúng như tôi dự đoán ban đầu, khi dùng War.hs để bet thử, chương trình sẽ gửi liên tiếp những request với số xu >2000 tới server, và server KHÔNG check kịp!
Nếu gửi từng request riêng lẻ, Tcp Server sẽ biết 1 người chơi đã đặt cược số xu tối đa, nhưng nếu gửi đi với tốc độ cực nhanh thì Tcp Server sẽ nhận hết và ko kiểm tra kịp. Hehe, điểm ăn tiền là đây.

Tôi đã học cách dùng forkIO và forM_ từ 2 gói Control.Monad và Control.Concurrent, rất quan trọng đối với người mới học nhé. Tôi thực sự ấn tượng với forkIO của Haskell, nhờ nó, mà threading dễ dàng hơn bao giờ hết. Ngạc nhiên thay, forkIO chiếm rất ít bộ nhớ.

Về sau tôi còn được nếm trải các bài học về kiểm soát Threads, dùng threadDelay, close Thread, handle 1000+ threads... nhờ vào việc viết tool cheat game này.

---

# Bắt đầu công việc làm ăn

Nhóm chat của tôi gồm Rin, Cherry, Hanso4 và tôi. Tôi thông báo cho mọi người về việc đã có thể cheat được Game X.

***Cherry*** lúc này đang làm Mod quản lý fanpage, group đã giúp tôi thông tin từ ban điều hành Game.

***Rin*** giúp tôi tìm bug game, việc bug bạc vô tận chính là do lão kiếm thông tin được. Tôi viết tính năng này vài phút :)

***Hanso4*** đợt trước hắn ôm rất nhiều acc cùi Vip3, bây giờ là lúc phát huy tác dụng.

Tôi bug 1 lượng bạc cực lớn cho nhóm, và bắt đầu bug Xu từ việc cá cược.

Tôi cũng rao bán tool trong 1 group kín khác. Lúc này ngocpck bay vào topic bán tool và sỉ vả như 1 kẻ bề trên, hắn vẫn nghĩ chỉ có một mình phe hắn là có tool, còn tôi chỉ là lừa đảo. Khi tôi chụp ảnh bằng chứng bug xu trong game, hắn lập tức thay đổi thái độ, lúc này hắn lại nghi rằng tôi "ăn cắp" tool từ bên hội a-e phương Bắc -))

Tôi cũng giao 2 bản tool cho Cherry và Rin để 2 người thực hành, còn Hanso4 lúc này đã qua Nhật, tình hình bên đó căng nên hắn chỉ mua Clone giúp nhóm. Mua 1 lần 150 clone vip3 cơ. Rin thì bắt đầu bán Xu...

---

# Hoàn thành Tool

Những tuần sau đó tôi hoàn thành tool, thêm 1 số tính năng như cày level, cày bang, trảm ma... Rồi fix bug, beautify code, handle threads, reassign module, tuning performance...

Nhưng quan trọng nhất vẫn là bug bạc và cheat Xu liên chiến. Kể ra cái bug bạc cũng là 1 dạng lỗi "ngơ ngơ" của đội dev Game X.

10PM tối Chủ Nhật hàng tuần, các game thủ trong top10 Server sẽ được phát quà là Bạc. Khi nhận xong thì nút "Nhận thưởng" trong app game sẽ bị disable, ko lấy được nữa. Nhưng nếu fake request nhận bạc gửi tới Server thì vẫn nhận được. Lỗi nhỏ nhưng NPH lại ko đủ sức Fix, tôi nghĩ có lẽ NPH đã hết hạn hợp đồng với NSX Game bên tàu, nên chẳng ai giúp đỡ fix bug.

Bug bạc này cũng là bên phía mafia phương Bắc tìm ra, và tôi chỉ là người thực hiện lại. Có lẽ ko cần phải show code ở đoạn này nữa nhỉ.

Lỗi này cũng giúp tôi kiếm kha khá VNĐ ahihi, rủng rình 1-2m/tuần.