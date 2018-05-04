---
layout: post
title: "Chapter 07: Unexpected Discoveries"
comments: true
description: "Nghệ thuật hắc ám - Phần 07: Những khám phá bất ngờ"
keywords: "haskell, pure, functional, hijack, game, server"
---

# Bug Tool hay Bug Game?

Trong thời gian dev tool, tôi nhận thấy nhiều điểm hơi vô lý của Game X, rất nhiều lỗ hổng có thể khai thác được. Có điểm tôi thử, có điểm tôi không.

Như tính năng cược Xu có 2 vấn đề mà Server cần kiểm tra tính hợp lệ:

* Tổng số Xu cược cho mỗi trận đấu, tối đa là 2000. Điều này tôi đã gian lận được bằng cách gửi thật nhanh các gói data để Server ko kịp kiểm tra toàn bộ.

* Số Xu đặt cược và tài sản của người chơi, bạn ko thể cược 1000 Xu nếu trong túi chỉ có 800 Xu. Điều này tôi có thử và ko thành công. Tuy nhiên tôi đã bỏ sót một trường hợp!

Tháng 11-2017, Rin có vào Saigon thông báo 1 tin sốc: Tool tôi viết có thể đánh lừa Server về số xu hiện có của người chơi.

Tôi rất ngạc nhiên, vậy nhưng Rin và Ace.Never đã dùng chính Tool tôi viết để khai thác được lỗ hổng này. Đôi khi, chính người dùng họ lại hiểu sản phẩm hơn là người phát triển các bạn ạ.

Điểm mấu chốt để lừa được Server là Stress-Test! Cũng tương tự như cách mà tôi vượt qua đoạn kiểm tra số xu đã cược của mỗi game thủ.

Ví dụ tôi có 1800 xu, tôi cược 2000 xu thì sẽ thất bại, Server check ngay khi nhận request. Thay vì vậy, tôi cược n lần 1000 xu, và phải thật nhanh, để Server chưa kịp hiểu ra. Khi đó Server liên chiến sẽ ghi nhận tôi đã cược n-lần 1000 xu, nhưng chỉ trừ Xu 1 lần duy nhất (thật ra thì làm gì còn xu để mà trừ, ahihi)

Vậy n là bao nhiêu? Qua nhiều lần benchmark, tôi ghi nhận được con số cao nhất mà tool của tôi có thể đánh lừa Server là 300 requests. Nếu mỗi request tôi đặt 1000 xu thì tương đương với số Xu gian lận được là 300.000. Tôi không chắc con số 300 requests đó phải là giới hạn cuối hay ko. Ví như tôi tuning performance thêm, hoặc ai đó viết được 1 tool khác ưu việt hơn, con số có phải là 500, hay 1000, maybe...

---

# Triệu phú "in-game"

Ban đầu, gói data cược xu được build như sau:

```haskell
bet1000 :: ByteString -> ByteString
bet1000 idx = C.append (hexSerialize $ C.length s) s
                where s = C.append "crossserverwar betting "
                        $ C.append idx " 1000\NUL"
```
Sau lần gặp Rin, cuối tuần đó tôi dùng 1acc còn ít xu, cỡ 3000, thử gửi 200 requests cược xu tới Server. Bingo! Server ghi nhận tôi đã cược 200.000 Xu.

Phải nói thêm về cái lỗi trời ơi này, nó sẽ giúp người chơi tay không bắt giặc. Game thủ ko cần phải me đến sát giờ chiến đấu để đặt cược nữa, và cũng không cần dùng acc phụ (Clone) để đặt vào bên thua. Bây giờ rất đơn giản, chỉ cần chọn kèo chắc ăn, đặt bên thắng, và đợi trận đấu kết thúc, easy Xu. Đây có thể gọi là dupe Xu.

Lần này tôi kỹ lưỡng hơn, sau khi nhận được 200k Xu từ lần dupe xu trên. Tôi tiếp tục thử một lỗ hổng khác, dùng function betX:

```haskell
betX :: ByteString -> ByteString
betX idx = C.append (hexSerialize $ C.length s) s
                where s = C.append "crossserverwar betting "
                        $ C.append idx " 150000\NUL"
```

Tôi nâng số xu 1 lần cược lên 150.000, và chỉ gửi 4 requests. Máy chủ ghi nhận tôi đã cược 600.000 Xu, trong túi vẫn còn dư lại 50k Xu. Wow, that's crazy!

Trên Client của Game X, người chơi chỉ có thể bấm chọn lượng xu cược là 100, 500, 1000 và 2000. Nhưng bây giờ, fake client của tôi gửi thành công cú cược xu huyền thoại 150k Xu :D. Nếu tận dụng triệt để 300 fake requests, vốn 150k thì số Xu tôi nhận được sẽ là 45 triệu Xu - con số khổng lồ.

Tôi dừng lại ở con số 600k Xu và thông báo với Rin về kết quả thử nghiệm. 2 người bọn tôi giữ kín lỗi này và cố gắng bán hết Clone Vip3.

---

# Phiên bản mở rộng

Thời điểm tháng 11, nhờ giá Xu giảm sâu, rất nhiều hảo thủ mới nổi, cuộc chiến giành ngôi Quán Quân bấy giờ rất khốc liệt. Các acc top có lực chiến gần bằng nhau có khi chỉ chiến thằng nhờ may mắn.

Phía bên ngocpck nghĩ ra trò mới là kết hợp phá top tiêu, top lật thẻ, kèm theo tặng bông ở trận đấu quyết định. Số bông được tặng cũng + thêm % sức mạnh cho đấu thủ liên chiến. Tôi cũng nhanh chóng cập nhật tính năng cày bông.

Ngocpck chuyển sang bán tướng. Đặc thù của Game X là tướng xịn thì rất đắt tiền và cần độ may mắn nữa mới chiêu mộ được. Nhưng ngocpck và minhchau tìm được lỗ hổng để lấy miễn phí. Thông tin lan đi, và tôi cũng code luôn tính năng mới này.

Nhưng về dupe xu, vẫn chỉ có tôi, Rin và Ace.Nver biết...

---

# Về minhchau đại ca

Một lần trong những cuộc đua cá cược Xu cuối tuần, ngocpck đã giở trò hèn hạ nhất: Dùng permanent key/time pair (tôi có giải thích ở phần trước) log vào acc đối thủ để phá hết Xu.

Cherry và XQ dính chưởng, vì acc của 2 bé này trước kia có mua xu bên a-e nhà ngocpck nên bị lưu cặp key/time.

Kể ra thì lỗi thuộc về minhchau trước, anh lưu toàn bộ thông tin acc mỗi lần bán xu!

Về minhchau đại ca, tôi và Rin đều nể vì anh mới chính là người viết ra tool đầu tiên của game. Cũng là người có tuổi, anh ít lên tiếng trong group, và còn thường xuyên giúp đỡ Rin...

Minhchau viết tool là để thử thách bản thân, anh ko bán mặc dù được trả giá cao. Về sau, minhchau có tâm sự với tôi là việc anh giao tool cho ngocpck là một sai lầm ko thể sửa chữa...