---
layout: post
title: "Chapter 07: Expansion of the Core"
comments: true
description: "Nghệ thuật hắc ám - Phần 07: Phiên bản mở rộng"
keywords: "haskell, pure, functional, hijack, game, server"
---

# Bug Tool hay Bug Game?

Thật ra trong lúc dev tool, tôi nhận thấy nhiều điểm hơi vô lý của Game X, rất nhiều lỗ hổng có thể khai thác được. Có điểm tôi thử, có điểm tôi không.

Như tính năng cược Xu, tôi nhận thấy có 2 vấn đề mà Server cần kiểm tra tính hợp lệ:

* Số Xu tối đa được phép cược, phải nhỏ hơn 2000 cho mỗi trận. Điều này tôi đã gian lận được bằng cách gửi thật nhanh các gói data để Server ko kịp kiểm tra toàn bộ.

* Số Xu cần thiết để cược, giả sử bạn có 1800 Xu, thì bạn ko thể cược được 2000. Điều này tôi có thử và ko thành công. Tuy nhiên tôi đã bỏ sót một trường hợp!

Tháng 11-2017, Rin có vào Saigon gặp tôi và nhắc tới vụ này, lão nói là Tool tôi viết có thể đánh lừa Server về số xu hiện có của người chơi.

Tôi rất ngạc nhiên, vậy nhưng Rin và Ace.Never đã dùng chính Tool tôi viết để khai thác đc lỗ hổng này. Đôi khi, chính người dùng họ lại hiểu sản phẩm hơn là nhà phát triển các bạn ạ.

Điểm mấu chốt để lừa được Server là Stress-Test! Cũng tương tự như cách mà tôi vượt qua đoạn kiểm tra số xu đã cược của mỗi game thủ.

Ví dụ tôi có 1800 xu, tôi cược 2000 xu thì sẽ thất bại, Server check ngay khi nhận request. Thay vì vậy, tôi cược n lần 1000 xu, và phải thật nhanh, để Server chưa kịp hiểu ra. Khi đó Server liên chiến sẽ ghi nhận tôi đã cược n-lần 1000 xu, nhưng chỉ trừ Xu 1 lần duy nhất (thật ra thì làm gì trừ được nữa, có mà âm Xu ahihi)

Vậy n là bao nhiêu? Qua nhiều lần benchmark tool, tôi ghi nhận được con số cao nhất mà tool của tôi có thể đánh lừa Server là 300 requests. Nếu mỗi request tôi đặt 1000 xu thì tương đương với số Xu gian lận được là 300.000. Tôi không chắc con số đó 300 requests đó phải là giới hạn cuối hay ko. Ví như tôi tuning performance thêm, hoặc ai đó viết được 1 tool khác ưu việt hơn, con số có phải là 500, hay 1000, maybe...

---

# Con số khổng lồ

Ban đầu, gói data cược xu được build như sau:

```haskell
bet1000 :: ByteString -> ByteString
bet1000 idx = C.append (hexSerialize $ C.length s) s
                where s = C.append "crossserverwar betting "
                        $ C.append idx " 1000\NUL"
```
Sau lần gặp Rin, cuối tuần đó tôi ngay lập tức dùng 1acc còn ít xu, cỡ 3000 thử gửi 200 requests cược xu tới Server. Bingo! Server ghi nhận tôi đã cược 200.000 Xu.

Phải nói thêm về cái lỗi trời ơi này, nó sẽ giúp người chơi tay không bắt giặc. Game thủ ko cần phải me đến sát giờ chiến đấu để đặt cược nữa, và cũng không cần dùng acc phụ (Clone) để đặt vào bên thua. Bây giờ rất đơn giản, chỉ cần chọn kèo chắc ăn, đặt bên thắng, và đợi trận đấu kết thúc, easy Xu. Đây có thể gọi là dupe Xu.

Lần này tôi kỹ lưỡng hơn, sau khi nhận được 200k Xu từ kèo dupe xu. Tôi tiếp tục thử một lỗ hổng khác, nếu may mắn tôi sẽ là đại gia vô đối trong Game luôn. Lần này tôi sửa lại function bet:

```haskell
betX :: ByteString -> ByteString
betX idx = C.append (hexSerialize $ C.length s) s
                where s = C.append "crossserverwar betting "
                        $ C.append idx " 150000\NUL"
```

Tôi nâng số xu 1 lần cược lên 150.000, và chỉ gửi 4 requests. Máy chủ ghi nhận tôi đã cược 600.000 Xu. Wow, dream come true!

Trên Client của Game X, người chơi chỉ có thể bấm chọn lượng xu cược là 100, 500, 1000 và 2000. Nhưng bây giờ, fake client của tôi gửi thành công cú cược xu huyền thoại 150k Xu :D. Nếu tận dụng triệt để 300 fake requests, vốn 150k thì số Xu tôi nhận được sẽ là 45 triệu Xu. Con số khổng lồ.

Tôi dừng lại ở con số 600k Xu và thông báo với Rin về kết quả mới. 2 người bọn tôi giữ kín lỗi này và cố gắng bán hết Clone Vip3.

---

# Phiên bản mở rộng

Thời điểm tháng 11, nhờ giá Xu giảm sâu, rất nhiều acc nổi lên và cuộc chiến giành ngôi Quán Quân mọi cấp độ bấy giờ rất khốc liệt. Các acc top có lực chiến gần bằng nhau có khi chỉ chiến thằng nhờ may mắn. Phía bên ngocpck nghĩ ra trò mới là kết hợp phá top tiêu, top lật thẻ, kèm theo tặng bông ở trận đấu quyết định. Số bông được tặng cũng + thêm % sức mạnh cho đấu thủ liên chiến.

Tôi cũng nhanh chóng cập nhật tính năng cày bông.

Ngocpck chuyển sang bán tướng. Đặc thù của Game X là tướng xịn thì rất đắt tiền và cần độ may mắn nữa mới chiêu mộ được. Nhưng ngocpck và minhchau tìm được lỗ hổng để lấy miễn phí. Thông tin lan đi, và tôi cũng code luôn tính năng mới này.

Nhưng về dupe xu, vẫn chỉ có tôi, Rin và Ace.Nver biết, cả 3 vẫn im lìm.

---

# Về minhchau đại ca
