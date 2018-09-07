---
layout: post
title: "Road to Blockchain: A Piece of History"
comments: true
description: "Road to Blockchain: Một phần của lịch sử"
keywords: "blockchain, bitcoin, history, satoshi, accounting, crypto"
---

![A piece of History](/assets/images/rtb01/history.png)

Satoshi Nakamoto - là ai nhỉ? Nghe quen quen. Xời, click click 2 nhát và đã có kết quả: Cha đẻ của Bitcoin - Yeah, một đồng tiền đắt giá. Vậy còn "blockchain" là sao nữa? Có phải công nghệ đắt giá gì ko? Ai là cha đẻ của nó, cũng là Satoshi sao?

Đúng, chính lão là người tạo ra blockchain đầu tiên. Nhưng hôm nay tôi muốn mời các bạn cùng du hành ngược thời gian để có cái nhìn khác về nguồn gốc của "Blockchain" - một công nghệ đã xuất hiện khá lâu nhưng vẫn tồn tại nhiều băn khoăn, hoài nghi xung quanh nó: Blockchain là gì? Đến từ đâu? Giải quyết vấn đề gì? Có đáng tin cậy ko? v.v...

Bài viết mở đầu series, là câu chuyện về sự ra đời của Blockchain: Từ những nhu cầu ghi chép đơn sơ đến một hệ thống lưu trữ tối ưu..

---

## 1. Từ nhu cầu ghi chép đơn sơ

Xin ngược dòng lịch sử một chốc, về thời kỳ săn bắn hái lượm luôn cho xa nhé :)

...

Thuở săn bắn ấy, tôi đi bẫy chồn, cả nhà ăn chồn 2 tuần nay đã ngán lắm, đi ngang nhà tên hàng xóm, thấy nó đang nướng cá thơm lừng. Tôi dụ dỗ nó đổi chác. Tên hàng xóm đồng ý, chồn đổi cá. Vậy đó, giao dịch đã xảy ra - trước cả khi con người biết đọc, ko chừng trước cả khi biết nói (who's know? hahaa)

Một ngày đẹp trời khác, tôi săn đc cả cọp Siberia, voi Mammoth, đương nhiên là ăn không hết. Nhưng tủ lạnh lại chưa đc phát minh nên cũng chẳng còn cách nào - ngoài đem cho thằng hàng xóm hoặc linh cẩu ăn bớt. Ngay cả khi, tôi đem đổi thành cá, chuối, heo rừng... thì cũng ko thể nhai hết được.

Và thế là, vỏ sò, vỏ hến trở thành đơn vị quy đổi cho hàng hóa. Tất nhiên phải là vỏ sò được mài thật đẹp, phụ nữ mang làm trang sức được mới có giá trị. Tôi săn đc cọp Siberia, để lại cái tay cọp cả nhà ăn lẩu, còn lại đem đổi lấy trăm vỏ sò ở ngoài chợ. Bữa nào đói quá, lười quá, hay say lá đu đủ quá ko săn được gì, tôi đem ít vỏ sò này đổi lấy vài chục trái táo, đôi con cá về ăn, vỏ sỏ quả là phát minh vĩ đại -))

![Ancient Egypt bazaar](/assets/images/rtb01/ancient_egypt_bazaar.jpg)

Rồi giao thương cũng từ đó mà vươn xa. Cọp Siberia đem xuống đồng bằng đổi sữa dê đùi ngựa, tôm cua đem lên cao nguyên đổi thịt voi, cafe đổi hồ tiêu, lúa gạo đổi máy bay, v.vv. Vỏ sò cũng tiến hóa thành tiền đồng, bạc, vàng, ngân phiếu, và cuối cùng thành 1 vài con số thập phân trong "tài khoản ngân hàng" - đó là chuyện về sau.

### Cuốn sổ ghi nợ

Khi "tiền vỏ hến" được sử dụng trong giao dịch, mọi người bắt đầu "ghi chép": để tính toán giá cả, theo dõi tài sản, và có lẽ cũng là để tiện đòi nợ. Ai đó đã phát minh ra chữ viết và giấy da, chính là sự khởi đầu cho sự bùng nổ của lĩnh vực ghi chép, lưu trữ thông tin. Đối với hoạt động buôn bán, các gian thương thời kỳ này sẽ có 1 cuốn sổ ghi chép những thứ như:

```haskell
-- Ngày 01, bán 10 đầu tôm được 100 sò, bán 16 mực khổng lồ được 400 sò, mua 2 bò con hết 600 sò.
-- Ngày 02, bán 20 cá thu được 200 sò, mua 2 cân gạo hết 40 sò.
```

Đây được coi là gốc rễ của ngành "kế toán - ghi sổ", hệ thống sổ ghi đơn giản như trên gọi là "Single-entry bookkeeping system". Các loại sổ ghi nợ, nhật ký buôn bán của gian thương về sau được đặt tên là Sổ Cái (Ledger).

---

## 2. Hệ thống ghi Sổ Kép

Khi thương mại vượt xa giới hạn bộ tộc, làng xã, tới quốc gia, vượt đại dương, xuyên lục địa... Hệ thống Sổ Đơn kia bộc lộ vấn đề về tính đúng đắn, minh bạch: không có một căn cứ nào để xác nhận việc ghi chép trên sổ là chính xác...

Hôm nay Cáo bán nợ cho Trâu già chục táo chín, vài hôm sau qua trả nợ thì Cáo bảo "Mày mua 12 trái lận, tao có ghi sổ đây...". Tranh cãi nổ ra và Trâu già húc lòi ruột Cáo, hết đời gian thương. Đó là vấn đề của Hệ thống Sổ Đơn.

### Giải pháp thay thế cho "Sổ đơn"

Giai đoạn đầu Trung cổ, người Do Thái bắt đầu tiên phong đổi mới ngành kế toán: Ghi Sổ Kép. Và sau đó ở Ý, Ghi Sổ Kép được xem như là chuẩn mực trong giao thương (đâu đó ở Thế Kỷ 15).

Về nguyên tắc, Ghi Sổ Kép là cách ghi dữ liệu debit (ghi nợ) và credit (ghi có) vào account (tài khoản) sao cho đảm bảo sự cân bằng của 2 phần này. Đọc thêm về [Hệ thống ghi Sổ kép](https://en.wikipedia.org/wiki/Double-entry_bookkeeping_system)

Lúc này, Trâu già mua chục trái táo của Cáo, thì giao dịch sẽ được ghi 2 lần:

```haskell
--Sổ của Cáo thêm 1 dòng: Ngày xx, bán cho Trâu già 10 trái táo, thu về 120 xu. --> Credit Account Cáo + 120
--Sổ của Trâu thêm 1 dòng: Ngày xx, mua của Cáo già 10 trái táo, mất 120 xu. --> Debit Account Trâu + 120
```

Như vậy đảm bảo Credit Cáo = Debit Trâu, và nếu cần thiết, 2 bên kí tên vào 1 bản hợp đồng chung, để khỏi ai giả mạo sổ sách hí hí. Và sau này có tranh cãi kiện tụng, cứ đem sổ sách ra nói chuyện, ko cần phải đụng răng đụng sừng :)

![Early 19th-century ledger](/assets/images/rtb01/ledger.png)

---

## 3. Yếu kém của Sổ Kép và các bổ sung

Cho tới bây giờ: 2018, chúng ta vẫn đang sử dụng cách ghi sổ có tuổi đời hơn 500 năm, vẫn và đã có những gian lận xảy ra. 

Vấn đề là Sổ Kép có một khiếm khuyết nằm ở 2 chữ Cân Bằng - "Balanced but it's not correct"

Debit và Credit phải cân bằng ư? Ko sao cả, đã từng có nhiều vị đại hiệp có khả năng phù phép sự cân bằng này bằng cách cố tình ghi chép sai, khai khống, mua chuộc, giả mạo chữ ký v.v... và những sai sót này được tính toán rất tỉ mỉ, công phu, đảm bảo "Totally Balanced" cho các tài khoản được ghi chép.

Ngành kiểm toán đã phát hiện được rất nhiều gian lận và chúng ta hằng ngày vẫn chứng kiến những phiên tòa xử các vụ án giả mạo sổ sách..

### Đặt niềm tin vào bên thứ 3

Những vụ án giả mạo và gian lận xảy ra, khiến Trâu già ko còn tin tưởng bạn làm ăn của mình. Trang trại súc vật lúc này, nổi lên họ nhà Vượn, nổi tiếng khéo léo, thông minh, biết tổ chức và hơn hết là "đáng tin cậy".

Giao dịch diễn ra ở trang trại đa phần sẽ thông qua họ nhà Vượn.

Trâu già muốn mua nhãn của Khỉ-đột, thì sẽ nói với nhà Vượn 1 tiếng - rằng hắn sắp mua của Khỉ 2 cân nhãn, giá đồng ý là 40xu. Vượn sẽ làm chứng cho giao dịch này, và sẽ ghi vào sổ của nhà Vượn 1 dòng ghi chép:

```haskell
--Ngày xx, Trâu già mua của Khỉ-đột 2 cân táo, giá 40xu.
```

Trâu già và Khỉ-đột cũng đồng thời ghi chú vào sổ của mình giao dịch trên.

Như vậy, cách mà nhà Vượn tham gia vào ghi chép cho giao dịch của Trâu và Khỉ, được coi là một phương pháp tiếp cận bổ sung cho nền tảng Ghi Sổ Kép. Cách tiếp cận này tin cậy hơn, giảm thiểu rủi ro của sai sót và gian lận, và mang tính chất lưu trữ - phòng trường hợp tranh chấp, thanh tra..

Đây là cách mà Ngân Hàng hoạt động, dĩ nhiên, nhà Vượn (a.k.a Ngân Hàng) sẽ thu một mức phí để duy trì hoạt động làm "bên thứ 3 tin cậy" này.

### Kỷ nguyên số hóa

Cùng với vòng xoáy của Computer và Internet, công nghệ lưu trữ số hóa cũng được áp dụng vào ghi chép.

+ Computer tính toán thay cho con người.
+ Hard Disk lưu trữ thông tin thay cho sổ sách, giấy tờ.
+ Chữ ký tay được thay bằng chữ ký số.
+ Bank account được sử dụng rộng rãi và tiện dụng nhờ Internet.
...

Thời điểm này, Ngân Hàng và các Tổ chức tín nhiệm khác cũng đã số hóa phần lớn sổ sách và ghi chép.

---

## 4. Lưu trữ thông tin thời kỳ hiện đại

Đọc tới đây, các bạn cũng hiểu lĩnh vực ghi chép, lưu trữ đã có một lịch sử rất thú vị như vậy, nó luôn luôn có khiếm khuyết, và con người cũng chưa bao giờ ngừng hoàn thiện nó. Những công nghệ mới, tiêu chuẩn mới, phát minh mới vẫn cứ xuất hiện theo thời gian...

Đột phá trong lĩnh vực CNTT mang đến những hệ thống lưu trữ thông tin giao dịch khổng lồ, tập trung, được quản lý bởi những Tổ chức tín nhiệm (Trusted Third Party).

Tất nhiên, TTP cũng có nhiều nhược điểm, và đáng kể nhất có lẽ là hiểm họa "Insider Fraud" - Gian lận nội bộ.

![Insider Fraud](/assets/images/rtb01/cyber_attack.jpg)

Nói một cách dễ hiểu, là những gian lận này phát sinh từ bản thân "bên trong tổ chức" mà chúng ta đang tin tưởng. Chúng ta đang đặt niềm tin vào những tổ chức tín nhiệm, họ thường mang danh tiếng và của cải ra để đảm bảo cho sự tín nhiệm của tổ chức. Nhưng "tổ chức" đó là ai? Cũng là những con người bình thường mà thôi..

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

---

## 5. Một hệ thống ghi chép hoàn hảo

Nhận thấy những hiểm họa về an toàn thông tin và mặt trái của nguyên lý tập trung trong những Tổ chức tín nhiệm, chúng ta lại một lần nữa đi tìm giải pháp cho một nền tảng lưu trữ mới...

Có một sự thật rằng, khi người nào đó tìm ra được một lỗ hổng của hệ thống, thì chính người đó cũng đồng thời nghĩ tới giải pháp khắc phục. Hơn ai hết, họ là người hiểu rõ bản chất vấn đề nhất.

Từ những năm 198x, rất nhiều nhà nghiên cứu đã đóng góp vào quá trình cải tiến hệ thống ghi chép, lưu trữ, thanh toán, mã hóa... Gián tiếp lẫn trực tiếp, lý thuyết và thử nghiệm... Các bạn có thể xem thêm ở đây: [Satoshi Nakamoto Institute](https://nakamotoinstitute.org/literature/), một số bài nổi bật tôi gợi ý nên đọc:

1. [Nick Szabo - The God Protocols (1997-1999)](https://nakamotoinstitute.org/the-god-protocols/)

2. [Nick Szabo - Bit Gold (2005)](https://nakamotoinstitute.org/bit-gold)

3. [Hal Finney - For-Pay Remailers (1994)](https://nakamotoinstitute.org/for-pay-remailers)

4. [Hal Finney - RPOW Reusable Proofs of Work (2004)](https://nakamotoinstitute.org/rpow/)

5. [Ian Grigg - Triple Entry Accounting (2005)](https://nakamotoinstitute.org/triple-entry-accounting)

Note: Nghiên cứu của Ian Grigg hoàn toàn ko liên quan đến lý thuyết "Momentum Accounting and Triple-Entry Bookkeeping" của giáo sư Yuji Ijiri. Có một blog trên hackernoon đã viết sai về khái niệm "kế toán tam phân", người dịch Việt ngữ cũng sai theo.

Tóm tắt lại cho các bạn ko có thời gian đọc, những nghiên cứu khoảng thời gian này, ít nhiều đều hướng đến một hệ thống lưu trữ hoàn thiện, mang các đặc điểm:

- Tính phân tán và minh bạch: Sổ Cái sẽ được lưu làm nhiều bản, đồng bộ và nằm ở nhiều nơi khác nhau.

- Tính toàn vẹn: mỗi thông tin (giao dịch) được lưu vào sổ thì không có cách nào chỉnh sửa, thay đổi.

- Tính tự chủ: Cơ chế đồng thuận/xác minh ngang hàng và công bằng, nhằm loại bỏ bên bên thứ 3 (hệ thống tín nhiệm).

### Sự ra đời của bitcoin/blockchain

Và cuối năm 2008, Satoshi đại hiệp đã mang đến hệ thống thanh toán "như yêu cầu": Bitcoin!

Bitcoin ra đời để khẳng định tính khả thi của tiền số (Electronic Cash or Digital Cash) nhưng đồng thời (vô tình ??) nó cũng là một giải pháp cho lưu trữ thông tin. Phương thức hoạt động của bitcoin như sau:

> Các dữ liệu giao dịch xảy ra trong một khoảng thời gian nhất định được gom lại thành 1 block, sau đó block này sẽ được "hash" (một dạng mã hóa) vào chain (là một chuỗi các blocks xảy ra trước đó). Bitcoin network sẽ đảm bảo chain-of-blocks này được cập nhật và đồng bộ theo thời gian, gần-như-ko-thể bị sửa đổi, không bị phụ thuộc bất kỳ Tổ chức nào khác.

--> Bạn đã hiểu nguồn gốc tên gọi "blockchain" ra đời ntnao rồi đó.

![Blockchain](/assets/images/rtb01/blockchain.jpg)

Blockchain đã xuất hiện như vậy, ko phải một ý tưởng chói lòa đến từ tương lai, mà là cả một quá trình nghiên cứu, hoàn thiện một nền tảng công nghệ ghi chép - lưu trữ dựa trên những điểm yếu của chính hệ thống hiện tại. Người ta đã nghiên cứu nó từ thập niên 80, và vẫn ko có dấu hiệu ngừng lại, khi hàng loạt công ty công nghệ lớn, ngân hàng, tập đoàn xuyên quốc gia, và cả chính phủ cũng đã bắt đầu tìm hiểu, nghiên cứu, thử nghiệm blockchain.

Xin dẫn một số use-case của blockchain, [từ website của IBM](https://www.ibm.com/blockchain/use-cases/):

1. [Ứng dụng blockchain vào hồ sơ y tế và dữ liệu y học lâm sàng](https://www-01.ibm.com/common/ssi/cgi-bin/ssialias?htmlfid=KU912404USEN)

2. [Ứng dụng trong an toàn thực phẩm và tra cứu nguồn gốc](https://www-03.ibm.com/press/us/en/pressrelease/53013.wss)

3. [Hệ thống thông tin định danh và tài sản cá nhân dựa trên blockchain](https://www-01.ibm.com/common/ssi/cgi-bin/ssialias?htmlfid=KU912405USEN)

4. [Tiền kỹ thuật số và hệ thống thanh toán mới](https://www-03.ibm.com/press/us/en/pressrelease/53290.wss)

5. [Quản lý mạng lưới năng lượng kiểu phân tán](https://www-03.ibm.com/press/us/en/pressrelease/52243.wss)

6. [Đổi mới trong quản lý quỹ đầu tư](https://www.youtube.com/watch?time_continue=1&v=uXx2vpDngPU)

...

Và còn rất nhiều ứng dụng tiềm năng khác, đang đợi những người tiên phong phát triển...

# References

https://bitcoin.org/bitcoin.pdf

https://resources.sei.cmu.edu/asset_files/Brochure/2012_015_001_28207.pdf

https://nakamotoinstitute.org/literature/

http://iang.org/ssl/pki_considered_harmful.html

https://www.ibm.com/blockchain/use-cases/

https://en.wikipedia.org/wiki/Double-entry_bookkeeping_system