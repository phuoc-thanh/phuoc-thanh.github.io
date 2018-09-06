---
layout: post
title: "Road to Blockchain: How it works?"
comments: true
description: "Road to Blockchain - Những khái niệm cơ bản"
keywords: "blockchain, proofofstake, proofofwork, bitcoin"
---

[Draft version - to be completed]

Ở bài viết mở đầu, tôi đã giới thiệu về một phần lịch sử của blockchain, về nền tảng để hình thành nên một hệ thống lưu trữ thông tin toàn vẹn. Chúng ta hiểu blockchain ra đời để xóa bỏ 2 thứ: gian lận trong ghi chép và bên thứ 3, nhưng làm cách nào để hiện thực hóa lý tưởng?

Bài viết thứ 2 trong series, tôi xin mô tả các đặc điểm của blockchain và cách hoạt động của một hệ thống mẫu (bitcoin)

## Blockchain characteristics

Nhắc lại về câu hỏi "blockchain là gì?"

Nói tóm gọn, blockchain là một hệ thống lưu trữ thông tin phân tán, ko phụ thuộc vào bất kỳ bên thứ 3 nào và đảm bảo được sự toàn vẹn của dữ liệu. Blockchain được xây dựng dựa trên 3 đặc điểm chính:

1. Distrubuted Ledger: Dữ liệu được ghi vào nhiều sổ khác nhau, và hoàn toàn giống nhau. Điều này góp phần loại bỏ một trung tâm lưu trữ tập trung và khiến cho hệ thống dữ liệu khó bị chỉnh sửa, đảm bảo an toàn đối với rủi ro mất mát thông tin.

2. Immutable Data: Mỗi ghi chép được dán nhãn, mã hóa và liên kết chặt chẽ với nhau khiến cho việc chỉnh sửa ghi chép gần như là điều bất khả thi.

3. Consensus Protocols: Cơ chế đồng thuận cởi mở...

### Blockchain và Bitcoin là 2 hay là 1?

Bitcoin ra đời để khẳng định tính khả thi của tiền số (Electronic Cash or Digital Cash). Satoshi giới thiệu một giải pháp cho vấn đề "double-spending" trong các giao dịch tiền số ngang hàng. Giải pháp này dựa trên cơ chế xác nhận phi tập trung và mã hóa các giao dịch vào một chuỗi gần-như-ko-thể-bị-đảo-ngược. Bitcoin là giải pháp cho tiền số nhưng vô tình (not sure) nó cũng là một giải pháp cho lưu trữ, nếu thay các dữ liệu giao dịch (transactions) bằng các bản ghi chép (records).

Chi tiết hơn về giải pháp của Bitcoin, nó bao gồm:

1. Proof-of-Work based Consensus Protocol: Cơ chế đồng thuận dựa trên PoW cho phép giao dịch được xác nhận mà ko cần dựa vào bên thứ 3. Ngoài ra, các bên tham gia mạng lưới sẽ có sổ cái riêng (phi tập trung), những sổ cái này đồng bộ về dữ liệu (same data)

2. Hashed transactions into an ongoing chain: Các dữ liệu giao dịch được hash (1 dạng mã hóa) vào 1 chuỗi có kèm thông tin thời gian, khiến các giao dịch này ko thể bị chỉnh sửa. Trong thực tế, các dữ liệu giao dịch này được gom lại thành 1 block, sau đó block này sẽ được hash vào chain --> Bạn đã hiểu nguồn gốc tên gọi blockchain ra đời ntnao rồi đó.

...

## Distributed Ledger Sytem

...

## Immutable Data

...

## Consensus Protocols


# Proof of Work - the need of

Hẳn các bạn còn nhớ tới phát minh vỏ sò ở phần trước chứ?

Chúng ta thử suy luận, tại sao nó phải được mài nhỏ, có thể là khắc lên nữa rồi mới có thể đem ra làm tiền giao dịch được?

Vì công việc mài dũa/điêu khắc một vỏ sò, vỏ hến đến một mức thật đẹp, thật tinh xảo sẽ chiếm một phần công sức, có thể đo đếm được - tất nhiên chỉ ở một mức độ tương đối. Nhưng khi cầm trên tay chiếc vỏ sò thật đẹp, nó là bằng chứng rằng người tạo ra nó ko chỉ dạo một vòng biển nhặt lên, mà người đó đã trải qua một quá trình làm việc, bỏ công sức chế tác để tạo ra chiếc vỏ sò có thể giao dịch được. Và người ta công nhận công sức của anh ta qua chiếc vỏ sò đó.

Vỏ sò, đó là nguyên mẫu rất xa xưa của cái gọi là "Proof of Work" / bằng chứng công việc.

Vậy nếu như một người nhặt được chiếc vỏ sò đẹp tự nhiên, như đã được chế tác rồi thì sao? Thì mọi người vẫn công nhận, may mắn cũng là một phần của hệ thống :)

Và vài trăm năm nay, những hệ thống Proof Of Work vẫn đang được sử dụng rất nhiều. Chúng ta có thể đang gián tiếp sử dụng nó mỗi ngày, nhưng ko ai để ý mà thôi.


# Hashcash by Adam Back (1997)

Wiki link: https://en.wikipedia.org/wiki/Hashcash

Quay trở lại kỉ nguyên số, năm 1997 Adam Back đưa ra hệ thống Hashcash, là một hệ thống xác nhận bằng chứng công việc (PoW system) và chuyên dùng để loại bỏ spam mail, tương tự như ví dụ trên để loại bỏ binh đoàn xin-ăn.

Hashcash yêu cầu bên người gửi phải đưa ra bằng chứng rằng họ "có bỏ công sức" ra khi gửi email đi. Và người nhận email sẽ xác nhận bằng chứng đó. "Bằng chứng công sức" này là một vài phép tính toán được cpu thực hiện.

Hashcash đảm bảo: đối với người sử dụng máy tính cá nhân, gửi đi 1 email-có-bằng-chứng-no-spam, thì công sức bỏ ra để tạo bằng chứng này vừa phải, không đáng kể so với cpu. Và đối với người nhận, việc xác nhận bằng chứng này cực kỳ dễ dàng. Nhưng đối với spammer, họ sẽ phải bỏ ra công sức rất lớn để đạt được yêu cầu của hệ thống hashcash.

**Nguyên lý hoạt động**

Cũng như nền tảng của hệ thống Proof-of-Work, hashcash sẽ có 1 cơ chế khiến người gửi phải hoạt động để đạt được 1 kết quả nào đó, ở trường hợp này, đó là một loại mã hash.

Loại mã hash này chỉ có 1 cách duy nhất để tìm ra là đoán dần: brute force, ko có cách tìm nào khác. Nhưng khi tìm ra rồi thì việc xác nhận độ đúng đắn của mã hash này rất dễ dàng.

**Phân tích kĩ thuật**

Hashcash - sử dụng thuật toán SHA-1 để mã hóa một chuỗi thông tin kèm bằng chứng công việc vào header của email. Và người nhận sẽ xác nhận bằng chứng này.

header của email sẽ có dạng:

`X-Hashcash: 1:20:1303030600:adam@cypherspace.org::McMybZIhxKXu57jd:ckvi`

Các thông tin chứa trong header gồm địa chỉ email, ngày gửi, và thông tin về bằng chứng công việc. Sự có mặt của địa chỉ email người nhận để đảm bảo rằng header này được tính toán dành cho mỗi người nhận cụ thể. Thời gian đính kèm để đảm bảo rằng email được gửi gần đây và để chắc chắn về header email: là duy nhất cho mỗi email


***Sender Side:***

Người gửi sẽ random 1 con số gắn vào header như trên và tính SHA (160bit) hash của header. Nếu 20 bits đầu tiên (5 hex digits) đều bằng zero, thì số hash này được coi là 1 bằng chứng "đạt chuẩn", sẽ được chấp thuận. Nếu không có kết quả như yêu cầu trên, sender sẽ tăng phần counter lên và tính hash lại. Xác suất để sender tính được số hash chuẩn ngay lần đầu tiên là 1/1 048 576. Đây cũng là trung bình số lần mà sender cần thử để tìm ra bằng chứng công việc - hash chuẩn.

Đối với máy tính cá nhân thông thường, đây là mức tính toán có thể chấp nhân được đối với 1 người sử dụng phổ thông, nhưng với spammer thì con số phép tính sẽ cực kỳ lớn bởi số lượng email spam.

***Receiver Side:***

Người nhận sẽ tính SHA của header và kiểm tra xem 20 bits đầu chuỗi hash có phải là zero không. Việc này chỉ mất 2 microsecond mà thôi. Nếu kết quả đúng thì sẽ tiếp tục kiểm tra các thông tin khác trong header như email address, time, database... để chắc chắn đây là email hợp lệ. Việc này cũng chiếm rất ít tài nguyên cpu và disk.


# Bitcoin PoW system (2009)

Bitcoin là một trong những công nghệ ứng dụng Proof of Work và Hashcash.

Bitcoin áp dụng hệ thống PoW để giải quyết vấn đề của giao dịch tiền, và loại bỏ bên thứ 3 là ngân hàng.

Bitcoin cũng dựa trên những nguyên lý của Adam's Hashcash để ứng dụng vào hệ thống xác nhận các giao dịch giữa người gửi và nhận. Tất nhiên phương pháp tính toán có thay đổi, phức tạp hơn, mạnh mẽ hơn, chặt chẽ hơn, khó bị bẻ gãy hơn. Nhưng về nguyên lý thì bitcoin cũng đang áp dụng 1 hệ thống tem (timestamp) tương tự hashcash.

Bitcoin cũng đc xem là ứng dụng tiên phong nhất của Blockchain, ở đây có 2 điều mà nhiều người lầm tưởng về bitcoin:

1. Bitcoin là một (trong rất nhiều) ứng dụng của blockchain - chứ ko phải blockchain là "duy nhất" bitcoin

2. Proof-of-Work cũng là một (trong rất nhiều) phương pháp để triển khai blockchain - chứ ko nhất thiết phải dùng PoW


# Proof of Stake

**Proof-of-Work problem**

Thật ko may, hệ thống PoW vẫn có những điểm yếu của riêng nó. Và "Năng lượng" chính là bài toán lớn nhất của 1 hệ thống PoW.

Cpu dùng để tìm mã hash cần sử dụng điện năng. Và điện năng tiêu thụ ngày một lớn khi nhu cầu sử dụng tăng. Ngta đang tự hỏi rằng họ tiêu thụ một lượng điện năng lớn để đáp ứng yêu cầu của hệ thống PoW liệu có phải là tối ưu? Liệu có giải pháp nào đó ưu việt hơn, hiệu năng cao hơn ko?

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

https://www.ibm.com/blogs/cloud-computing/2017/04/11/characteristics-blockchain/
