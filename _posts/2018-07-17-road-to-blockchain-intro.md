---
layout: post
title: "Road to Blockchain: A Piece of History"
comments: true
description: "Road to Blockchain: Một phần của lịch sử"
keywords: "blockchain, bitcoin, history, satoshi, accounting, crypto"
---

![A piece of History](/assets/images/rtb01/history.png)

Satoshi Nakamoto cùng câu chuyện đắt giá: Bitcoin, có lẽ đã ko còn quá xa lạ trong giới công nghệ nữa, vậy "Blockchain" thì sao? Có phải công nghệ đắt giá gì ko? Cũng là Satoshi phát minh ra hay sao?

Đúng, Satoshi là người tạo ra blockchain đầu tiên, nhưng sự xuất hiện Blockchain Technology ko chỉ đơn thuần xoay quanh bitcoin, mà xuất phát từ những yêu cầu đa dạng đối với việc lưu trữ thông tin như: An toàn, minh bạch, riêng tư, giảm thiểu chi phí...

Thực tế, những yêu cầu này đã thúc đẩy nhiều phát minh lớn trong ngành công nghệ thông tin, chính những phát minh đó mới là nền tảng cho sự xuất hiện của Blockchain.


---

## 1. Ngành Kế Toán và Hệ thống Sổ Kép

Trong quá khứ, nhu cầu giao-dịch-thương-mại là yếu tố ảnh hưởng rất lớn đến sự phát triển của công nghệ lưu trữ thông tin. Một trong số những văn bản cổ xưa nhất trong ngành thương mại phải kể đến, là Sổ Cái/Sổ ghi nợ (a.k.a **Ledger**). Nó ra đời để phục vụ việc tính toán giá cả, kiểm kê tài sản, và có lẽ cũng là để tiện đòi nợ.

Đại loại, gian thương sẽ ghi chép những thứ như:

```haskell
-- Nhật ký
-- ...
-- Ngày xx, bán 10 đầu tôm được 100 sò, bán 16 mực khổng lồ được 400 sò, mua 2 bò con hết 600 sò.
-- Ngày yy, bán 20 cá thu được 200 sò, mua 2 cân gạo hết 40 sò.
-- ...
```

Đây được coi là gốc rễ của ngành "kế toán - ghi sổ", hệ thống ghi sổ đơn giản như trên gọi là **Single-entry bookkeeping system**.

Về sau vỏ sò, vỏ hến, đá trang sức được thay thế bằng kim loại hiếm, bằng tiền, tín dụng... câu chuyện rất dài, nếu hứng thú, bạn có thể đọc thêm về [Money & Banking - tiền bối Giang Lê](https://kinhtetaichinh.blogspot.com/2010/12/money-and-banking-vii.html) có viết rất chi tiết. Sổ cái, tất nhiên cũng trải qua nhiều giai đoạn bổ sung và nâng cấp.. cho đến khi nó chỉ là những 'bit' nhị phân, ở năm hai không mười tám hiện tại.

### Hệ thống ghi Sổ Kép và Tín nhiệm

Cùng với sự mở rộng qui mô thương mại, ngân hàng và tiền giấy dần phổ biến trong giao thương, hệ thống sổ đơn cũng trở nên lỗi thời vì thiếu độ tin cậy. Người Do Thái bắt đầu tiên phong đổi mới ngành kế toán bằng Sổ Kép, rồi đâu đó Thế Kỷ 15, Sổ Kép trở thành chuẩn mực kế toán mới ở Italia.

Về nguyên tắc, [Hệ thống Sổ Kép](https://en.wikipedia.org/wiki/Double-entry_bookkeeping_system) là cách ghi dữ liệu debit (ghi nợ) và credit (ghi có) vào account (tài khoản) sao cho đảm bảo sự cân bằng của 2 phần này.


Lúc này, một giao dịch sẽ được ghi ít nhất 2 lần, ví dụ với một giao dịch mua bán 10 trái táo:

```haskell
--Sổ của Cáo thêm 1 dòng: Ngày xx, bán cho Trâu già 10 trái táo, thu về 120 xu. --> Credit Account Cáo + 120
```

```haskell
--Sổ của Trâu thêm 1 dòng: Ngày xx, mua của Cáo già 10 trái táo, mất 120 xu. --> Debit Account Trâu + 120
```

Như vậy đảm bảo Credit Cáo = Debit Trâu, và nếu cần thiết, 2 bên kí tên vào 1 bản hợp đồng chung, để khỏi ai giả mạo sổ sách hí hí.

![Early 19th-century ledger](/assets/images/rtb01/ledger.png)

Tín nhiệm trong giao dịch cũng ra đời sau đó ít lâu, khởi đầu bằng những tiệm ký gửi vàng - Goldsmith, và tiến hoá dần thành Ngân Hàng và tiền tệ. Ngân Hàng được xem như một tổ chức tín nhiệm - bên thứ ba, đem uy tín ra để lưu trữ tài sản, đồng thời ghi chép giao dịch và tình trạng tài sản của người tham gia giaiao dịch trong hệ thống.


---

## 2. Yếu kém của Sổ Kép và Tổ chức tín nhiệm

Cho tới hiện tại, chúng ta vẫn đang sử dụng cách ghi sổ kép có tuổi đời hơn 500 năm, và đã có những gian lận xảy ra. 

Vấn đề của Sổ Kép nằm ở 2 chữ Cân Bằng - "Balanced but it's not correct"

Có rất nhiều vị đại hiệp có khả năng phù phép sự cân bằng của Sổ kép này bằng cách cố tình ghi chép sai, khai khống, mua chuộc, giả mạo chữ ký v.v... và những sai sót này được tính toán tỉ mỉ, công phu, đảm bảo "Totally Balanced" cho các tài khoản được ghi chép.


### Hiểm hoạ gian lận nội bộ

Vai trò của Tổ chức tín nhiệm (Trusted Third Party) trong giao dịch, ban đầu được xem như một bổ sung, để giảm thiểu rủi ro của sai sót và gian lận, và mang tính chất lưu trữ - phòng trường hợp tranh chấp, thanh tra.. đúng như ý nghĩa câu nói "chọn mặt gửi vàng".

Thế kỷ 20, đột phá trong lĩnh vực CNTT mang đến những hệ thống lưu trữ thông tin giao dịch khổng lồ, tập trung, được quản lý bởi những Tổ chức tín nhiệm.
Tất nhiên, TTP cũng có nhiều nhược điểm, và đáng kể nhất có lẽ là hiểm họa "Insider Fraud" - Gian lận nội bộ.

![Insider Fraud](/assets/images/rtb01/cyber_attack.jpg)

Nói một cách dễ hiểu, là những gian lận này phát sinh từ bản thân "bên trong tổ chức" mà chúng ta đang tin tưởng. Chúng ta đang đặt niềm tin vào những tổ chức nơi mà họ thường mang danh tiếng và của cải ra để đảm bảo cho sự tín nhiệm của họ. Nhưng "tổ chức" đó là ai? Cũng là những con người bình thường mà thôi.

Những người bên trong một Tổ chức tín nhiệm, họ có thẩm quyền, họ được tiếp xúc với những dữ liệu ghi chép, hệ thống thông tin quan trọng. Và họ cũng chính là nguy cơ tiềm ẩn. Nhân viên cũ, cộng tác viên, đối tác, quản trị viên và thậm chí là kiểm soát viên đều có thể trở thành nhân tố tham gia vào những cuộc gian lận như:

- Thay đổi, chỉnh sửa chứng từ, ghi chép.
- Đánh cắp thông tin nhạy cảm (như tài khoản ngân hàng).
- Giả mạo sổ sách.
- Sử dụng trái phép tài sản ko thuộc sở hữu.
- Vi phạm tính riêng tư của người dùng
...

Các bạn có thể xem qua một nghiên cứu nhỏ của viện nghiên cứu công nghệ phần mềm SEI (Carnegie Mellon Uni) về gian lận nội bộ trong ngành tài chính ở [đây](https://resources.sei.cmu.edu/asset_files/Brochure/2012_015_001_28207.pdf)

### Trên sân chơi Internet

Ngoài lĩnh vực lưu trữ/xác nhận thông tin truyền thống, các Tổ chức tín nhiệm - TTP cũng được tin tưởng trên sân chơi khác là Internet: VISA, Verisign, Internet DNS, Paypal, C.A... Chúng ta không thể phủ nhận những lợi ích từ TTP mang lại, đặc biệt khi họ ứng dụng những công nghệ mã hóa hiện đại (Modern Cryptography) để đảm bảo an toàn thông tin cho người sử dụng. Nhưng niềm tin vào họ vẫn bị thử thách.

Các nhà nghiên cứu độc lập đã nhận diện được hiểm họa từ khá sớm, và vẫn liên tiếp xuất bản những nghiên cứu chung + riêng đề cập đến những mặt tối của "Trusted Third Party" thời kỳ Internet này. Scandal 2013 của Snowden, tuy muộn nhưng cũng góp phần khẳng định mối họa TTP là có thật.

Vì chủ đề gói gọn trong phạm vi blockchain, nên tôi dẫn nguồn nghiên cứu của 2 tác giả được cho là ảnh hưởng lớn tới sự ra đời của blockchain là Ian Grigg và Nick Szabo:

1. Những rào cản về chi phí, kĩ thuật, hạ tầng... chưa được dỡ bỏ kèm theo những lỗ hổng bảo mật của TTP: [Trusted Third Parties Are Security Holes - Nick Szabo](https://nakamotoinstitute.org/trusted-third-parties)

2. Tác hại của hệ thống khóa công khai (Public Key Infrastructure): [PKI considered harmful - Ian Grigg](http://iang.org/ssl/pki_considered_harmful.html)

Ở nghiên cứu của Ian Grigg về hệ thống PKI, có một đoạn ngắn mô tả một tác hại khác của TTP: nguyên tắc tập trung. Đó là khi TTP được trao một quyền lực quá lớn, gần như là độc quyền thì cũng chính là lúc giá trị của niềm tin (trust) dần bị loại bỏ. Người sử dụng sẽ ko có sự lựa chọn nào khác ngoài việc bắt buộc phải tin những Tổ chức này!

> ...Indeed, as he (Trusted Third Party) has total power over issuance of certificates, he is now a major source of weakness, placing great stress on the word 'trust'.

> This alternate logic has been expressed in the term Centralised Vulnerability Party or CVP. Instead of the marketing hope that you trust the TTP, you the user are forced to trust. You have no choice, and are vulnerable to this central, all-powerful party...

Một nguy cơ bảo mật khác của TTP là Single Point of Failure cũng thường được đề cập đến, nói đơn giản thì dữ liệu tập trung ở một nơi thì đồng nghĩa với rủi ro mất mát / ngưng hoạt động của toàn hệ thống nếu như điểm tập trung đó bị phá vỡ (bởi những cuộc tấn công, bởi hiểm hoạ tự nhiên, phá hoại nội bộ...).


---

## 3. Một hệ thống ghi chép hoàn hảo

Để khắc phục những nguy cơ về an toàn thông tin như đã kể trên, rất nhiều nghiên cứu và thử nghiệm được tiến hành, đặc biệt là ở 2 lĩnh vực: Mã hoá thông tin và phân tán dữ liệu.

Trong số những giải pháp về lưu trữ số, có rất nhiều nghiên cứu đã ảnh hưởng đến sự ra đời của bitcoin, như:

1. [Nick Szabo - The God Protocols (1997-1999)](https://nakamotoinstitute.org/the-god-protocols/)

2. [Nick Szabo - Bit Gold (2005)](https://nakamotoinstitute.org/bit-gold)

3. [Hal Finney - For-Pay Remailers (1994)](https://nakamotoinstitute.org/for-pay-remailers)

4. [Hal Finney - RPOW Reusable Proofs of Work (2004)](https://nakamotoinstitute.org/rpow/)

5. [Ian Grigg - Triple Entry Accounting (2005)](https://nakamotoinstitute.org/triple-entry-accounting)

**Note: Nghiên cứu của Ian Grigg hoàn toàn ko liên quan đến lý thuyết "Momentum Accounting and Triple-Entry Bookkeeping" của giáo sư Yuji Ijiri. Có một blog trên hackernoon đã viết sai về khái niệm "kế toán tam phân", người dịch Việt ngữ cũng đã hiểu sai về khái niệm này.**

Tóm tắt lại cho các bạn ko có thời gian đọc, những nghiên cứu khoảng thời gian này, ít nhiều đều hướng đến một hệ thống lưu trữ hoàn thiện, mang các đặc điểm:

- Tính phân tán: Sổ Cái sẽ được lưu làm nhiều bản, đồng bộ và nằm ở nhiều nơi khác nhau.

- Tính toàn vẹn: mỗi thông tin (giao dịch) được lưu vào sổ thì không có cách nào chỉnh sửa, thay đổi.

- Tính tự chủ: Cơ chế hoạt động ngang hàng, nhằm loại bỏ bên bên thứ 3 (hệ thống tín nhiệm).

### Sự ra đời của bitcoin/blockchain

Và cuối năm 2008, Satoshi đại hiệp đã mang đến một cuốn Sổ Cái "như yêu cầu": Bitcoin!

Bitcoin ra đời để khẳng định tính khả thi của tiền số (Electronic Cash or Digital Cash) nhưng đồng thời (vô tình ??) nó cũng là một giải pháp cho lưu trữ thông tin. Phương thức hoạt động của bitcoin như sau:

> Các dữ liệu giao dịch xảy ra trong một khoảng thời gian nhất định được gom lại thành 1 block, sau đó block này sẽ được "hash" (một dạng mã hóa) vào chain (là một chuỗi các blocks xảy ra trước đó). Bitcoin network sẽ đảm bảo chain-of-blocks này được cập nhật và đồng bộ theo thời gian, gần-như-ko-thể bị sửa đổi, không bị phụ thuộc bất kỳ Tổ chức nào khác.

Bạn đã hiểu tên gọi "blockchain" (a.k.a chain-of-blocks) có nguồn gốc từ đâu rồi đó.

![Blockchain](/assets/images/rtb01/blockchain.jpg)

Blockchain đã xuất hiện như vậy, ko phải một ý tưởng chói lòa đến từ tương lai, mà là cả một quá trình nghiên cứu, hoàn thiện một nền tảng công nghệ ghi chép - lưu trữ dựa trên những điểm yếu của chính hệ thống hiện tại. Người ta đã nghiên cứu nó từ thập niên 80, và vẫn ko có dấu hiệu ngừng lại, khi hàng loạt công ty công nghệ lớn, ngân hàng, tập đoàn xuyên quốc gia, và cả chính phủ cũng đã bắt đầu tìm hiểu, nghiên cứu, thử nghiệm blockchain.

Các bạn có thể xem [Khảo sát toàn cầu về Blockchain của Deloitte - 2018](https://www2.deloitte.com/content/dam/Deloitte/us/Documents/financial-services/us-fsi-2018-global-blockchain-survey-report.pdf) để thấy bức tranh toàn cảnh về trạng thái hiện tại của công nghệ blockchain.

Hoặc bạn cũng có thể tham khảo thêm các giải pháp cụ thể trên nền tảng blockchain [của IBM](https://www.ibm.com/blockchain/use-cases/)

...

Và còn rất nhiều ứng dụng tiềm năng khác, đang đợi những nhà phát triển tiên phong...


---

## References

https://bitcoin.org/bitcoin.pdf

https://resources.sei.cmu.edu/asset_files/Brochure/2012_015_001_28207.pdf

https://nakamotoinstitute.org/literature/

http://iang.org/ssl/pki_considered_harmful.html

https://www.ibm.com/blockchain/use-cases/

https://en.wikipedia.org/wiki/Double-entry_bookkeeping_system

https://www2.deloitte.com/content/dam/Deloitte/us/Documents/financial-services/us-fsi-2018-global-blockchain-survey-report.pdf
