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

Mỗi nhát cuốc được bổ xuống, cảm biến bên trong cuốc sẽ hoạt động và tìm kiếm 1 loại đá đặc biệt (Crypton chẳng hạn, hehe). Các kĩ sư thiết đã đo đạc và tính toán rất kĩ mật độ của loại đá này trong nền địa chất của mỏ kim cương, và cho ra 1 con số thích hợp. Ví dụ, tỉ lệ xấu nhất để cảm biến tìm thấy được loại đá này là 12000 cuốc, và trường hợp may mắn cuốc lần đầu đã trúng thì cực kỳ thấp. Trung bình thợ đào sẽ cuốc đc 14000 nhát trong 8 tiếng làm việc, như vậy rất dễ dàng để đo được là chủ cây cuốc có làm việc hay không.


Hệ thống xác nhận bằng chứng công việc kiểu này được gọi là Proof of Work (system)!



# Hashcash by Adam Back (1997)

Wiki link: https://en.wikipedia.org/wiki/Hashcash

Quay trở lại kỉ nguyên số, năm 1997 Adam Back đưa ra hệ thống Hashcash, là một hệ thống xác nhận bằng chứng công việc (PoW system) và chuyên dùng để loại bỏ spam mail, tương tự như ví dụ trên để loại bỏ binh đoàn xin-ăn.

Hashcash yêu cầu bên người gửi phải đưa ra bằng chứng rằng họ "có bỏ công sức" ra khi gửi email đi. Và người nhận email sẽ xác nhận bằng chứng đó. "Bằng chứng công sức" này là một vài phép tính toán được cpu thực hiện.

Hashcash đảm bảo: đối với người sử dụng máy tính cá nhân, gửi đi 1 email-có-bằng-chứng-no-spam, thì công sức bỏ ra để tạo bằng chứng này vừa phải, không đáng kể so với cpu. Và đối với người nhận, việc xác nhận bằng chứng này cực kỳ dễ dàng. Nhưng đối với spammer, họ sẽ phải bỏ ra công sức rất lớn để đạt được yêu cầu của hệ thống hashcash.

**Nguyên lý hoạt động**

Cũng như nền tảng của hệ thống Proof-of-Work, hashcash sẽ có 1 cơ chế khiến người gửi phải hoạt động để tìm 1 thứ gì đó đặc biệt, ở trường hợp này, đó là một loại mã (hash) thay vì crypton :)

Loại mã hash này chỉ có 1 cách duy nhất để tìm ra là đoán dần: brute force, ko có phương pháp thay thế nào khác. Nhưng khi tìm ra rồi thì việc xác nhận độ đúng đắn của mã hash này rất dễ dàng.

**Phân tích kĩ thuật**

Hashcash - sử dụng thuật toán SHA-1 để mã hóa một chuỗi thông tin kèm bằng chứng công việc vào header của email. Và người nhận sẽ xác nhận bằng chứng này.

header của email sẽ có dạng:

`X-Hashcash: 1:20:1303030600:adam@cypherspace.org::McMybZIhxKXu57jd:ckvi`

> ver: Hashcash format version, 1 (which supersedes version 0).

> bits: Number of "partial pre-image" (zero) bits in the hashed code.

> date: The time that the message was sent, in the format YYMMDD[hhmm[ss]].

> resource: Resource data string being transmitted, e.g., an IP address or email address.

> ext: Extension (optional; ignored in version 1).

> rand: String of random characters, encoded in base-64 format.

> counter: Binary counter (up to 220), encoded in base-64 format.

Các thông tin chứa trong header gồm địa chỉ email, ngày gửi, và thông tin về bằng chứng công việc. Sự có mặt của địa chỉ email người nhận để đảm bảo rằng header này được tính toán dành cho mỗi người nhận cụ thể. Thời gian đính kèm để đảm bảo rằng email được gửi gần đây và để chắc chắn về header email: là duy nhất cho mỗi email


Sender Side:

Người gửi sẽ random 1 con số gắn vào header như trên và tính SHA (160bit) hash của header. Nếu 20 bits đầu tiên (5 hex digits) đều bằng zero, thì số hash này được coi là 1 bằng chứng "đạt chuẩn", sẽ được chấp thuận. Nếu không có kết quả như yêu cầu trên, sender sẽ tăng phần counter lên và tính hash lại. Xác suất để sender tính được số hash chuẩn ngay lần đầu tiên là 1/1 048 576. Đây cũng là trung bình số lần mà sender cần thử để tìm ra bằng chứng công việc - hash chuẩn.

Đối với máy tính cá nhân thông thường, đây là mức tính toán có thể chấp nhân được đối với 1 người sử dụng phổ thông, nhưng với spammer thì con số phép tính sẽ cực kỳ lớn bởi số lượng email spam.

Receiver Side:

Người nhận sẽ tính SHA của header và kiểm tra xem 20 bits đầu chuỗi hash có phải là zero không. Việc này chỉ mất 2 microsecond mà thôi. Nếu kết quả đúng thì sẽ tiếp tục kiểm tra các thông tin khác trong header như email address, time, database... để chắc chắn đây là email hợp lệ. Việc này cũng chiếm rất ít tài nguyên cpu và disk.


# Bitcoin PoW system (2009)

Bitcoin là một trong những công nghệ ứng dụng Proof of Work và Hashcash.

Như đã giới thiệu ở phần nguyên lý hoạt động của hệ thống Proof-of-Work, lợi ích rõ ràng nhất mà hệ thống mang lại là loại bỏ bên thứ 3 (cai mỏ) ra khỏi việc giao tiếp, kiểm tra, thanh toán giữa chủ và nhân công.

Bitcoin áp dụng hệ thống PoW để giải quyết vấn đề của giao dịch tiền, và loại bỏ bên thứ 3 là ngân hàng.

Bitcoin cũng dựa trên những nguyên lý của Adam's Hashcash để ứng dụng vào hệ thống xác nhận các giao dịch giữa người gửi và nhận. Tất nhiên phương pháp tính toán có thay đổi, phức tạp hơn, mạnh mẽ hơn, chặt chẽ hơn, khó bị bẻ gãy hơn. Nhưng về nguyên lý thì bitcoin cũng đang áp dụng 1 hệ thống tem (timestamp) tương tự hashcash.

Bitcoin cũng đc xem là ứng dụng tiên phong nhất của Blockchain, ở đây có 2 điều mà nhiều người lầm tưởng về bitcoin:

1. Bitcoin là một (trong rất nhiều) ứng dụng của blockchain - chứ ko phải blockchain là "duy nhất" bitcoin

2. Proof-of-Work cũng là một (trong rất nhiều) phương pháp để triển khai blockchain - chứ ko nhất thiết phải dùng PoW


# Proof of Stake

**Proof-of-Work problem**

Thật ko may, hệ thống PoW vẫn có những điểm yếu của riêng nó. Và "Năng lượng" chính là bài toán lớn nhất của 1 hệ thống PoW.

Cảm biến nằm bên trong cán cuốc, cpu dùng để tìm mã hash, đều cần sử dụng điện năng. Và điện năng tiêu thụ ngày một lớn khi nhu cầu sử dụng tăng. Ngta đang tự hỏi rằng họ tiêu thụ một lượng điện năng lớn để đáp ứng yêu cầu của hệ thống PoW liệu có phải là tối ưu? Liệu có giải pháp nào đó ưu việt hơn, hiệu năng cao hơn ko?

Và khái niệm Proof of Stake ra đời, chủ yếu là để áp dụng trong lĩnh vực tiền mã hóa.

**Concept**

Proof of Stake được giới thiệu như là 1 cuộc chơi mới cho những người cùng sử dụng 1 hệ thống. Mỗi người trong hệ thống đều có 1 số cổ phần (stake), và họ tự xác nhận với nhau các bản ghi (thường là các bản ghi giao dịch)

Hệ thống PoS cũng loại bỏ bên thứ 3 như PoW, và nó ko yêu cầu người tham gia phải xử lý tính toán để xác nhận, mà chính họ tự xác nhận với nhau. Vậy làm sao để "họ tự xác nhận" với nhau đc?

Các hệ thống PoS thường phát hành 1 lượng coins/tokens nào đó tương tự như cổ phiếu, và những ai sở hữu coin/token này được coi là cổ đông, các cổ đông này sẽ tham gia quá trình xác nhận bản ghi (giao dịch...).

Hệ thống PoS lựa chọn người xác nhận 1 bản ghi dựa trên mức độ uy tín/giàu có thông qua lượng cổ phần nắm giữ. Thông thường những ai nắm nhiều cổ phần sẽ có lợi thế trong việc xác nhận, nhưng PoS có thêm các giao thức, quy tắc khác để đảm bảo tính ngẫu nhiên trong khâu chọn lựa người xác nhận kế tiếp - đảm bảo rằng ko phải cứ giàu nhất thì có 100% cơ hội được chọn.

Những cách thức đảm bảo cho sự ngẫu nhiên này có thể kể đến như: Randomized block selection, Coin Age based selection.

# Blockchain Revolution

Sự bùng nổ của blockchain cũng kéo theo rất nhiều vấn đề khác như tính bảo mật, tính riêng tư, mức độ khách quan, công bằng, sự chấp nhận và thích nghi của cộng đồng...

Chắc chắn có rất nhiều bài toán kĩ thuật khác cũng đang cần giải pháp. Chúng ta sẽ tiếp tục khám phá và giải mã những vấn đề này, trong phần kế tiếp :)

# References

https://bitcoin.org/bitcoin.pdf
https://en.wikipedia.org/wiki/Proof-of-work_system
https://en.wikipedia.org/wiki/Hashcash
https://en.wikipedia.org/wiki/SHA-2
