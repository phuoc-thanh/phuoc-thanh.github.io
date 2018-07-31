---
layout: post
title: "Road to Blockchain - Part 1: Proof of Work - What and How?"
comments: true
description: "Proof of Work - Những khái niệm cơ bản"
keywords: "blockchain, proofofstake, proofofwork, bitcoin"
---

# Proof of Work - the need of

Nếu tôi là chủ của 1 mỏ kim cương, cai quản hàng ngàn thợ đào mỏ, và tôi muốn có một cách thức chấm công tự động nào đó để không phải sử dụng nhiều cai mỏ.

Tôi làm sao biết được, đến cuối ngày anh thợ A, B đã đào cật lực, anh Y chỉ ngồi mát, thậm chí anh Z nào đó ko phải là công nhân của tôi mà chỉ đợi tới giờ phát lương là lẻn vào để nhận tiền công?

Tôi cần bằng chứng công việc: Hãy show bằng chứng rằng anh đã làm việc cật lực để nhận đc tiền công!

Tôi thuê một đội kĩ sư, họ phát minh ra cái cuốc thông minh, gắn 1 loại cảm biến có thể hiểu được người sử dụng cuốc có chịu làm việc hay không...

Hàng ngàn cái cuốc thông minh được phát cho công nhân đào mỏ, và tôi trả công cho thợ đào dựa trên bằng chứng của cuốc thông minh báo. Đảm bảo toàn bộ thợ đào đều phải làm việc và xứng đáng nhận được tiền công, ko ai có thể mạo danh để nhận công.

Cây cuốc này hoạt động như thế nào?

Mỗi nhát cuốc được bổ xuống, cảm biến bên trong cuốc sẽ hoạt động và tìm kiếm 1 loại đá đặc biệt (Crypton chẳng hạn, hehe). Các kĩ sư thiết đã đo đạc và tính toán rất kĩ mật độ của loại đá này trong nền địa chất của mỏ kim cương, và cho ra 1 con số thích hợp. Ví dụ, tỉ lệ xấu nhất để càm biến tìm thấy được loại đá này là 12000 cuốc, và trường hợp may mắn cuốc lần đầu đã trúng thì cực kỳ thấp. Trung bình thợ đào sẽ cuốc đc 14000 nhát trong 8 tiếng làm việc, như vậy rất dễ dàng để đo được là chủ cây cuốc có làm việc hay không.


Hệ thống xác nhận bằng chứng công việc kiểu này được gọi là Proof of Work (system)!



# Hashcash by Adam Back (1997)

https://en.wikipedia.org/wiki/Hashcash

Quay trở lại kỉ nguyên số, năm 1997 Adam Back đưa ra hệ thống Hashcash, là một hệ thống xác nhận bằng chứng công việc (PoW system) và chuyên dùng để loại bỏ spam mail, tương tự như ví dụ trên để loại bỏ binh đoàn xin-ăn.

Hashcash yêu cầu bên người gửi phải đưa ra bằng chứng rằng họ "có bỏ công sức" ra khi gửi email đi. Và người nhận email sẽ xác nhận bằng chứng đó. "Bằng chứng công sức" này là một vài phép tính toán được cpu thực hiện.

Hashcash đảm bảo: đối với người sử dụng máy tính cá nhân, gửi đi 1 email-có-bằng-chứng-no-spam, thì công sức bỏ ra để tạo bằng chứng này vừa phải, không đáng kể so với cpu. Và đối với người nhận, họ xác nhận bằng chứng này rất dễ dàng. Nhưng đối với spammer, họ sẽ bỏ ra công sức cực kỳ lớn để đạt được yêu cầu của hệ thống.

**Phân tích kĩ thuật**

Loại bằng chứng này chỉ có 1 cách duy nhất để tìm ra là đoán dần (brute force) để tìm ra. Nhưng khi tìm ra rồi thì việc xác nhận độ đúng đắn của nó rất dễ dàng.

Hashcash - sử dụng SHA-1 để mã hóa một chuỗi thông tin kèm bằng chứng công việc vào header của email. Và recipient sẽ xác nhận bằng chứng này.

header của email sẽ có dạng:

`X-Hashcash: 1:20:1303030600:adam@cypherspace.org::McMybZIhxKXu57jd:ckvi`

ver: Hashcash format version, 1 (which supersedes version 0).

bits: Number of "partial pre-image" (zero) bits in the hashed code.

date: The time that the message was sent, in the format YYMMDD[hhmm[ss]].

resource: Resource data string being transmitted, e.g., an IP address or email address.

ext: Extension (optional; ignored in version 1).

rand: String of random characters, encoded in base-64 format.

counter: Binary counter (up to 220), encoded in base-64 format.

The header contains the recipient's email address, the date of the message, and information proving that the required computation has been performed. The presence of the recipient's email address requires that a different header be computed for each recipient. The date allows the recipient to record headers received recently and to ensure that the header is unique to the email message.


Sender Side:

Người gửi sẽ random 1 con số gắn vào header như trên và tính SHA (160bit) hash của header. Nếu 20 bits đầu tiên (5 hex digits) đều bằng zero, thì số hash này được coi là 1 bằng chứng "đạt chuẩn", sẽ được chấp thuận. Nếu không có kết quả, sender sẽ tăng phần counter lên và tính hash lại. Xác suất để sender tính được số hash chuẩn ngay lần đầu tiên là 1/1 048 576. Đây cũng là trung bình số lần mà sender cần thử để tìm ra bằng chứng công việc - hash chuẩn.

Đối với máy tính cá nhân thông thường, đây là mức tính toán có thể chấp nhân được đối với 1 người sử dụng phổ thông, nhưng với spammer thì con số phép tính sẽ cực kỳ lớn bởi số lượng email spam.

Receiver Side:

Người nhận sẽ tính SHA của header và kiểm tra xem 20 bits đầu chuỗi hash có phải là zero không. Việc này chỉ mất 2 microsecond mà thôi. Nếu kết quả đúng thì sẽ kiểm tra các thông tin khác trong header như email address, time, database... để chắc chắn đây là email hợp lệ. Việc này cũng chiếm rất ít tài nguyên cpu và disk.


# Bitcoin PoW system (2008)

Bitcoin là một trong những công nghệ ứng dụng Proof of Work và Hashcash.


# References

https://bitcoin.org/bitcoin.pdf
https://en.wikipedia.org/wiki/Proof-of-work_system
https://en.wikipedia.org/wiki/Hashcash
https://en.wikipedia.org/wiki/SHA-2
