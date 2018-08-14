---
layout: post
title: "Road to Blockchain - The First Look"
comments: true
description: "Road to Blockchain - Bước ra từ lịch sử"
keywords: "blockchain, proofofstake, proofofwork"
---

Nói về một công nghệ mới mẻ, luôn là thách thức lớn đối với blogger, và nó là một loại công việc tiêu hao rất nhiều thời gian và công sức.
4 phần mày mò tìm hiểu, nhưng 6 phần quan trọng hơn là giải thích, diễn đạt để người đọc-nghe hiểu, mới là thành công của 1 bài viết.

Chủ đề lần này tôi chọn viết là một mảng công nghệ nhận được sự quan tâm rất lớn từ cộng đồng thời gian qua: Blockchain.

Có thể các bạn đã đọc rất nhiều, nghe rất nhiều, tìm tòi rất lâu nhưng vẫn đang bối rối với những gì thu thập được - như tôi. Thì hẳn bạn rất khao khát muốn biết rõ hơn về nguồn gốc, ý tưởng đằng sau blockchain, những thôi thúc nào đã giúp Satoshi tạo ra bitcoin? Blockchain - thật sự là công nghệ của tương lai hay chỉ là công cụ bánh vẽ của những con cá mập để thu lợi?

Bài viết đầu tiên trong series, sẽ tổng hợp và cố gắng giải thích những điều cơ bản nhất về blockchain, từ nhu cầu ghi chép đơn sơ nhất đến sự bùng nổ của công nghệ mã hóa. 

Vậy xin ngược dòng lịch sử một chốc, về thời kỳ săn bắn hái lượm luôn cho xa nhé :)

## 1. Từ nhu cầu ghi chép đơn sơ

Bắt đầu bằng một nhu cầu cơ bản khi con người sống tập trung là ***Trao đổi (Exchange)***

Hôm nay tôi săn đc con chồn, cả nhà ăn chồn 2 tuần nay đã ngán lắm, đi ngang nhà tên hàng xóm, thấy nó đang nướng cá, thơm lừng. Tôi bèn gợi ý đổi con chồn lấy 5 con cá của nó. Thằng hàng xóm đồng ý trao đổi, như vậy là đã xảy ra 1 giao dịch. Vậy đó, giao dịch đã xảy ra - trước cả khi con người biết đọc, ko chừng trước cả khi biết nói (who's know? hahaa)

Đến bước phát triển kế tiếp, là nhu cầu ***Buôn bán, giao thương (Trade)***

Một ngày đẹp trời, tôi săn đc 6 con chồn, hay thậm chí săn đc cả cọp siberia, voi mammoth, đương nhiên là ăn không hết, nhưng tủ lạnh lại chưa đc phát minh nên cũng chẳng còn cách nào - ngoài đem cho thằng hàng xóm hoặc linh cẩu ăn bớt. Ngay cả khi, tôi đem đổi thành cá, hay trái cây, thì cũng ko tài nào xơi hết được.

Và thế là, "vỏ sò" được phát minh ra, dùng để làm đơn vị quy đổi cho hàng hóa. Tiền thời này, là vỏ sò được mài thật đẹp, phụ nữ mang làm trang sức được. Tôi săn đc 1 cọp siberia, để lại cái tay cọp cả nhà ăn lẩu, còn lại tôi đem đổi lấy trăm vỏ sò ở ngoài chợ (chợ là mạng lưới trao đổi hàng hóa nhé). Bữa nào đói quá, lười quá, hay say lá đu đủ quá ko săn được gì, tôi đem ít vỏ sò này đổi lấy vài chục trái táo, đôi con cá về ăn, vỏ sỏ quả là phát minh vĩ đại -))

Rồi giao thương cũng từ đó mà vươn xa. Cọp siberian đem xuống đồng bằng đổi sữa dê đùi ngựa, tôm cua đem lên cao nguyên đổi thịt voi, cafe đổi hồ tiêu, lúa gạo đổi máy bay, v.vv. Và vỏ sò cũng tiến hóa thành tiền đồng, bạc, vàng, ngân phiếu, và tiến tới thành 1 vài con số thập phân trong "tài khoản ngân hàng" - đó là chuyện về sau.

### Cuốn sổ ghi nợ

Khi "tiền" được sử dụng trong giao dịch, mọi mua bán đều cần phải được ghi chép, để tính toán giá cả, theo dõi tài sản, và có lẽ cũng là để tiện đòi nợ. Ai đó đã phát minh ra chữ viết và giấy da, và từ "ghi sổ" cũng đồng thời đc đưa vào từ điển. Đại loại, các gian thương thời kỳ này sẽ có 1 cuốn sổ ghi chép những thứ như:

+ Ngày 01, bán 10 đầu tôm được 100 sò, bán 16 mực khổng lồ được 400 sò, mua 2 bò con hết 600 sò.
+ Ngày 02, bán 20 cá thu được 200 sò, mua 2 cân gạo hết 40 sò.
+ ...

Đây được coi là khởi đầu của ngành "kế toán - ghi sổ", hệ thống sổ ghi đơn giản như trên được coi là "Single-entry bookeeping system"


## 2. Hệ thống ghi Sổ Kép

Vấn đề của ghi Sổ Đơn là gì?

Khi thương mại vượt xa giới hạn bộ tộc, làng xã, tới quốc gia, vượt đại dương, xuyên châu lục... Cuốn Sổ Đơn kia bộc lộ vấn đề về tính đúng đắn, minh bạch - khi không có một căn cứ nào để xác định được việc ghi chép trên sổ là đúng, sẽ dẫn tới các vấn đề về xác định tài sản, giá cả, thuế má, gian lận thương mại...

Hôm nay Cáo bán nợ cho Trâu già chục táo chín, vài hôm sau qua trả nợ thì Cáo bảo "Mày mua 12 trái lận, tao có ghi sổ đây...". Tranh cãi nổ ra và Trâu già húc lòi ruột Cáo, hết đời gian thương. Đó là vấn đề của hệ thống sổ đơn.

***Giải pháp thay thế cho "Ghi sổ đơn"***

Giai đoạn đầu Trung cổ, người Do Thái bắt đầu tiên phong đổi mới ngành kế toán: ghi sổ kép. Và sau đó ở Ý, việc thực thi ghi sổ kép được đem ra làm chuẩn mực trong giao thương (đâu đó ở Thế Kỷ 15).

Về nguyên tắc, nó là cách ghi dữ liệu debit (ghi nợ) và credit (ghi có) vào account (tài khoản) sao cho đảm bảo sự cân bằng của 2 phần này. Đọc thêm về ghi sổ kép: [Link Wiki](https://en.wikipedia.org/wiki/Double-entry_bookkeeping_system)

Lúc này nhé, Trâu già mua chục trái táo của Cáo, thì:

Sổ của Cáo note: Ngày xx, bán cho Trâu già 10 trái táo, thu về 120 xu. --> Credit Account Cáo + 120

Sổ của Trâu note: Ngày xx, mua của Cáo già 10 trái táo, mất 120 xu. --> Debit Account Trâu + 120

Như vậy đảm bảo Credit Cáo = Debit Trâu, và nếu cần thiết, ta kí tên vào 1 bản hợp đồng chung, để khỏi ai giả mạo sổ sách hí hí. Và sau này có tranh cãi kiện tụng, cứ đem sổ sách ra nói chuyện, ko cần phải đụng răng đụng sừng :)

## 3. Yếu kém của Sổ Kép và các bổ sung

Vấn đề của ghi sổ kép là gì?

Cho tới bây giờ - 2018, chúng ta vẫn đang sử dụng cách ghi sổ có tuổi đời hơn 500 năm, vẫn và đã có những gian lận xảy ra. 

Vấn đề là Sổ Kép có một khiếm khuyết nằm ở 2 chữ Cân Bằng - "Balanced but it's not correct"

Debit và Credit phải cân bằng ư? Ko vấn đề gì, chúng ta có những thiên tài, địa tài hay đại hiệp ẩn danh có khả năng phù phép sự cân bằng này bằng cách cố tình ghi chép sai, khai khống, mua chuộc, giả mạo chữ ký v.v... và những sai sót này được tính toán rất tỉ mỉ, công phu, đảm bảo "Totally Balanced" cho các tài khoản được ghi chép.

Ngành kiểm toán đã phát hiện được rất nhiều gian lận về sổ sách kế toán, chúng ta hằng ngày vẫn chứng kiến những phiên tòa xử các vụ án giả mạo sổ sách..

### Đặt niềm tin vào bên thứ 3

Những vụ án giả mạo và gian lận xảy ra, khiến Trâu già ko còn tin tưởng bạn làm ăn của mình. Trang trại súc vật lúc này, nổi lên họ nhà Vượn, nổi tiếng khéo léo, thông minh, biết tổ chức và hơn hết là "đáng tin cậy".

Giao dịch diễn ra ở trang trại đa phần sẽ thông qua họ nhà Vượn.

Trâu già muốn mua nhãn của Khỉ-đột, thì sẽ nói với nhà Vượn 1 tiếng -  rằng hắn sắp mua của Khỉ 2 cân nhãn, giá đồng ý là 40xu. Vượn sẽ làm chứng cho giao dịch này, và sẽ ghi vào sổ của nhà Vượn 1 dòng ghi chép: 

> Ngày xx, Trâu già mua của Khỉ-đột 2 cân táo, giá 40xu.

Trâu già và Khỉ-đột cũng đồng thời ghi chú vào sổ của mình giao dịch trên.

Như vậy, cách mà nhà Vượn tham gia vào ghi chép cho 1 giao dịch của Trâu và Khỉ, được coi là một phương pháp tiếp cận bổ sung cho nền tảng Ghi Sổ Kép. Cách tiếp cận này tin cậy hơn, giảm thiểu rủi ro của sai sót và gian lận, và mang tính chất lưu trữ - phòng trường hợp tranh chấp, thanh tra..

Đây là cách mà Ngân Hàng hoạt động, dĩ nhiên, nhà Vượn (a.k.a Ngân Hàng) sẽ thu một mức phí để duy trì hoạt động làm "bên thứ 3 tin cậy" này.

### Kỷ nguyên số hóa

Cùng với vòng xoáy của Computer và Internet, công nghệ lưu trữ số hóa cũng được áp dụng vào ghi chép.

+ Nhập liệu Sổ sách giấy tờ được thay bằng Software, Hard Disk.
+ Chữ ký tay được thay bằng chữ ký số.
+ Bank account được sử dụng rộng rãi và tiện dụng nhờ Internet.
...

Thời điểm này, Ngân Hàng và các bên thứ 3 khác (Vượn đội lốt) cũng đã số hóa phần lớn sổ sách và ghi chép

## 4. Chữ ký số và Hóa đơn điện tử

**Vấn đề của bên thứ 3**

Đó là `Insider Fraud`, có thể dịch ra là gian lận nội bộ.

Gian lận xảy ra giữa người mua - kẻ bán, và đặc biệt là nằm ở bên thứ 3 - như nhà Vượn. Kể cả ghi chép giao dịch được ghi làm 3 bản, vẫn chưa đủ đảm bảo độ toàn vẹn dữ liệu.

Làm sao để chắc là Trâu già và Khỉ đột giữ ghi chép về việc mua bán? Thật sự mà nói, chúng ta đã đủ bận rộn rồi, không một ai ghi chép đầy đủ những giao dịch trong ngày, và chúng ta chọn cách tin tưởng tuyệt đối vào bên thứ 3 như Ngân Hàng, Chính Phủ...

Nếu một ngày bên thứ 3 xảy ra sai sót so với hợp đồng giao dịch của bên mua-bán, nếu 2 trong 3 bên quyết tâm làm méo mó những ghi chép thì sao? Hoặc rủi ro, toàn bộ sổ sách ở bên thứ 3 đột nhiên bị mất hết (chập điện, cháy nổ, thiên tai...) thì chuyện gì xảy ra?

Hay đơn giản hơn là sự sụp đổ - biến mất của bên thứ 3, ồ lúc này thảm họa ghi chép mới xuất hiện.

Và công nghệ mã hóa bước chân vào cuộc chơi..

### Triple entry accounting

Hoàn toàn ko liên quan đến lý thuyết "Momentum Accounting and Triple-Entry Bookkeeping" của giáo sư Yuji Ijiri, Nguyên lý kế toán mới của giáo sư là về dự đoán đà tăng trưởng. Tôi đang nhắc đến 1 paper của Ian Grigg xuất bản năm 2005.

Bài viết gốc ở [đây](https://nakamotoinstitute.org/triple-entry-accounting)

Nếu có một cách ghi sổ mà mọi người đều có thể xem được giao dịch ghi trong Sổ sách?

Nếu có một hệ thống mà mỗi giao dịch đã ghi thì ko thể nào bị chỉnh sửa?

Nếu có một hệ thống mà có một cơ chế đồng thuận tốt hơn, ko cần bên thứ 3 nhưng đảm bảo giao dịch được xác minh đúng đắn?

Nếu hệ thống xác minh hoạt động bền vững khó bị phá vỡ và đủ nhanh để sử dụng xuyên lục địa?

Hệ thống đó, nếu có, sẽ là Blockchain!

## 5. Blockchain

Toàn bộ những vấn đề trên đều liên quan tới giao dịch thương mại, tiền, nhưng hãy hình dung đến các khía cạnh khác có thể áp dụng "giao dịch" như:

+ Bỏ phiếu, nếu chúng ta vote xong thì coi như là 1 giao dịch sẽ được ghi vào sổ cái, kiểm phiếu minh bạch
+ Chấm bài thi
+ Quản lý định danh cho mỗi người
+ Sổ xố?

# References

https://bitcoin.org/bitcoin.pdf

https://hackernoon.com/why-everyone-missed-the-most-important-invention-in-the-last-500-years-c90b0151c169

https://nakamotoinstitute.org/triple-entry-accounting

https://en.wikipedia.org/wiki/Double-entry_bookkeeping_system