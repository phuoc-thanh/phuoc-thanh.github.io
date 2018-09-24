---
layout: post
title: "Road to Blockchain: How it works?"
comments: true
description: "Road to Blockchain - Nguyên lý hoạt động của blockchain"
keywords: "blockchain, proofofstake, proofofwork, bitcoin"
---

Như đã giới thiệu ở [bài viết trước](https://thanhdo89se.github.io/2018/road-to-blockchain-intro/), bitcoin ra đời để giải quyết vấn đề double-spending trong lưu hành tiền kỹ thuật số. Nhưng nó đồng thời mở ra một hướng tiếp cận mới cho các nền tảng lưu trữ hiện đại, dựa vào 3 đặc điểm: phân tán sổ sách, toàn vẹn dữ liệu, và tự chủ hệ thống.

Vậy bitcoin/blockchain thể hiện 3 đặc điểm đó ra sao? Và hiện thực hóa nó như thế nào? Chúng ta tiếp tục khám phá, lần này là về kiến trúc tổng quan của một mạng lưới Blockchain.

---

## 1. Phân tán và Đồng bộ hóa Sổ cái

Đầu tiên, hãy cùng đặt vấn đề với hệ thống lưu trữ hiện tại.

Những ghi chép quan trọng, phần nhiều vẫn sử dụng Hệ thống sổ kép có bổ sung bên thứ 3, Thông tin được ghi làm 3 bản: Bên A, Bên B, và xác nhận bên thứ 3. Ồ, có 3 bản thôi á? 3 bản thì làm sao mà yên tâm được đây?

Ko khó để tưởng tượng hoàn cảnh khi 1, 2 hay thậm chí là 3 bản ghi chép bị mất mát, sai sót. Và gian lận xảy ra, niềm tin bị thử thách, như đã nói ở bài trước.

### Vậy blockchain sao lưu dữ liệu như thế nào?

Blockchain đề xuất một giải pháp lưu trữ phân tán và đồng bộ. Nghĩa là, dữ liệu sẽ được lưu ở nhiều nơi khác nhau, được cập nhật theo thời gian đảm bảo toàn bộ sổ cái trong mạng sẽ lưu thông tin chính xác như nhau.

Một giao dịch thành công giữa tôi và bạn, tôi ghi vào sổ của tôi, bạn ghi vào sổ của bạn, vợ tôi cũng ghi, hàng xóm tôi cũng ghi, chú em con dì chị vợ của bạn cũng ghi, bà bán vé số cũng ghi, chủ tịch Quốc Hội cũng ghi, đến cả Cậu Vàng của Lão Hạc cũng sẽ ghi lại - nếu nó biết viết.

Vậy là, toàn bộ những ai tham gia vào mạng lưới đều cần phải ghi chép đủ các giao dịch vào sổ của họ, 3 người tham gia thì có 3 cuốn sổ, 1 triệu người tham gia thì có thể có 700 nghìn sổ hoặc 2 triệu sổ, điều đó ko ai biết, và chúng ta cũng chưa vội bàn tới.

### Phân tán sổ sách, thì được lợi ích gì?

Tất nhiên, càng nhiều bản sao, thì mất mát và sai sót thông tin càng khó xảy ra. Nice!

Tiếp, Ai cũng có quyền lưu trữ toàn bộ dữ liệu, nghĩa là mọi giao dịch đều minh bạch. Ai cũng có thể xem toàn bộ giao dịch từ xưa như trái đất cho tới hiện nay. Ơ, như vậy thì còn gì là riêng tư? Đừng quá lo lắng, người tham gia Blockchain network ko cần phải khai báo tên tuổi, gốc gác.

Cuối cùng, phi tập trung khiến cho hệ thống hoạt động bền vững và khó bị tấn công hơn. Ví dụ thế này cho dễ hiểu: Thay vì phải tập trung sức mạnh tấn công vào một trung tâm dữ liệu lớn, thì kẻ phá hoại giờ phải tìm diệt (hoặc mua chuộc) mạng lưới gồm vài trăm / vài triệu anh em đang núp sau màn hình ở hang hốc nào đó rải rác khắp quả đất.

### Lợi hại quá, nhưng bằng cách nào?

Câu trả lời là: Mạng-ngang-hàng, a.k.a Peer-to-peer network.

Ko có gì mới mẻ cả, tương tự như BitTorrent thoi, hehe. Bạn chưa biết BitTorrent và p2p network là gì? Ko sao, tôi mô tả luôn..

Thử nghĩ, bạn ngồi trước máy tính, và muốn nghe Bích Phương hát chẳng hạn, bạn thường tìm đến nhaccuitui, mp3zing để tải bài hát về hoặc nghe online (cũng là một hình thức tải về). Như vậy, mp3zing hay nhaccuitui, gọi chung là "Server" - đang phục vụ cả triệu lượt khách hàng giống như bạn mỗi ngày, đó chính là giao thức server-client điển hình của Internet hiện nay.

Rồi một ngày kia, Phương ko vui lòng, Phương bắt những Server này gỡ bài hát của Phương xuống, thì sẽ ko còn lần sau để mà nghe "Bùa Yêu" nữa. Yeah, lúc này muốn nghe Phương hát, hẳn là bạn phải kiếm ai đó để copy, bằng usb, bằng cáp chì, bằng bluetooth các kiểu, và sau đó bạn có thể chia sẻ các bài hát của Phương cho người khác nữa. Đây chính là giao thức peer-to-peer, ko ai phục vụ ai, ko ai quản lý - can thiệp nổi vào thứ mà mọi người đang chia sẻ.

BitTorrent là một sân chơi như vậy, một mạng lưới, mà các loại "file - tập tin" được chia sẻ ngang hàng, giữa những người tham gia vào mạng đó. Blockchain network thì ko chia sẻ bài hát hay phần mềm, mà nó chia sẻ sổ cái (Ledger). Giả sử bạn muốn tham gia vào mạng lưới blockchain, bạn chỉ cần cắm dây mạng và hô to câu thần chú "Hế lô, Xin-rô-nai Bờ-lốc-chên". Và 500ae sẽ dâng Ledger của họ đến tận nhà bạn.

---

## 2. Toàn vẹn dữ liệu

Về nhu cầu toàn vẹn dữ liệu, có lẽ ko cần phải nói thêm nữa, vì chắc ko ai muốn phải phí công phí sức để tìm hiểu những việc như: Bản sao này có giống bản chính ko? Số liệu này có bị ai đó chỉnh sửa ko? Giao dịch này là thật hay là giả? Sổ sách này có ghi chép đầy đủ ko? Chữ ký trên hợp đồng này có hợp lệ? Hóa đơn này có phải mới xuất hồi sáng nay?...

### Và blockchain đảm bảo toàn vẹn dữ liệu thật sao?

Đúng vậy, một khi dữ liệu được xác nhận trong mạng lưới blockchain, thì nó gần như là bất khả xâm phạm, ko thể bị chỉnh sửa.

Cuốn sổ cái blockchain là một cuốn sổ đặc biệt, mỗi khi bạn ghi chép 1 trang mới vào sổ thì mọi người sẽ đọc nội dung trang vừa được ghi đó, xác nhận nội dung xong thì họ sẽ dán một loại tem đặc biệt lên trang đó. Tem này đảm bảo trang giấy bạn vừa ghi **ĐÚNG ĐẮN**, và **HỢP LỆ**.

**Làm sao biết đó là cuốn sổ đúng đắn, và hợp lệ?**

Loại Tem nói trên đặc biệt ở chỗ, nó được tạo ra từ 2 thứ:

+ Nội dung của trang ứng với nó. Bạn chỉ cần thay đổi 1 kí tự trong trang thôi, thì blockchain-network khi đọc Tem này sẽ biết rằng nội dung bên trong trang đã bị thay đổi.
+ Tem của trang trước. Có nghĩa là các trang phải được sắp xếp theo đúng thứ tự. Việc đảo lộn hoặc xóa bớt trang bất kỳ, đều khiến cho Sổ cái của bạn ko hợp lệ với blockchain-network.

Ồ khoan đã, dừng lại si nghĩ thêm 1 chút nhé. Để đảm bảo được 2 đặc điểm trên, thì có phải, Tem này là **Duy Nhất** cho một trang cụ thể? Ko thể có trường hợp trùng lặp như Một trang sinh ra 2 tem khác nhau, hoặc 2 Trang khác nội dung sinh ra cùng 1 loại Tem?

### Lại câu hỏi cũ, bằng cách nào?

Cơ chế sinh Tem của Blockchain, ko phải chỉ là quảng cáo, nó thật sự đảm bảo được Một con Tem chỉ ứng với Một nội dung sinh ra nó. Kỹ thuật Mật Mã Học chính là nền tảng cho cơ chế hoạt động của Tem này. Xin giới thiệu chìa khóa cho các hoạt động đánh dấu/sinh Tem của blockchain: [Hàm băm Mật Mã Học](https://en.wikipedia.org/wiki/Cryptographic_hash_function).

Hàm băm, hay tiếng Anh "Hash Functions" là loại kỹ thuật ko mới mẻ đối với kỹ sư CNTT, đặc biệt trong lĩnh vực Bảo mật thông tin. Như cái tên của nó, Hash Function sẽ băm dữ liệu có sẵn thành 1 dòng mật mã - gọi là Mã Hash, đảm bảo Mã sinh ra là duy nhất cho nội dung dữ liệu. Bất kỳ thay đổi nào dù chỉ là dấu chấm, phẩy cũng đều làm Mã Hash thay đổi.

Và Hash Functions thuộc loại mã hóa một chiều. Bạn ko thể dịch ngược từ một Mã Hash thành nội dung ban đầu của nó được. Chắc là các bạn đã thấy ứng dụng rộng rãi nhất của nó: lưu trữ Password. Các website "đàng hoàng" sẽ ko bao giờ lưu password của người dùng, mà họ lưu Mã Hash của password.

Có một điểm lưu ý, về khả năng trùng lắp của hàm băm, hàm băm càng tốt, thì khả năng sinh Mã Hash trùng lặp càng nhỏ. Nếu tò mò về khả năng này, bạn hãy thử search cụm từ: "SHA256 Collision", SHA256 là một loại thuật toán để sinh ra tem của blockchain đó :)

**Một số cụm từ chuyên môn**

Bây giờ tôi sẽ trả lại nguyên bản những từ ngữ đã bị vay mượn:

```haskell
-- Sổ cái/Ledger:     Blockchain or Chain of Blocks
-- Trang của Sổ Cái:  Block in a Blockchain
-- Tem của một Trang: Block Hash of a Block
```

---

## 3. Tự chủ và cơ chế đồng thuận

Đọc đến đây, hẳn bạn vẫn chưa hoàn toàn bị thuyết phục, vẫn còn những điểm chưa-hợp-lý-lắm? 

Thứ Nhất, ai là người nhận trách nhiệm "Xác nhận và Đóng dấu" (Hash) dữ liệu? Một máy chủ tập trung à? Vậy đâu có khác Hệ thống tín nhiệm - Trusted Third Party đâu?

Thứ Hai, nếu cho là ai cũng Hash được dữ liệu của chính mình, thì sẽ có hàng ngàn phiên bản của Sổ cái, vậy làm thế nào để xác định đâu là Sổ Cái chuẩn nhất, để đồng bộ toàn mạng Blockchain? Lại một máy chủ tập trung khác?

**Blockchain thực sự cần thứ gì?**

Bây giờ, sau khi đã có p2p network hỗ trợ cho sự phân tán và Hash Functions đảm bảo tính toàn vẹn cho dữ liệu, blockchain cần có một cơ chế đồng thuận để giúp nó tự chủ, loại bỏ hoàn toàn vai trò của TTP ra khỏi cuộc chơi.

- Việc "Xác nhận" và "Đóng dấu" những ghi chép mới vào Sổ Cái là trách nhiệm của toàn bộ người tham gia blockchain-network. Quyết định Sổ Cái nào là hợp lệ, cũng là trách nhiệm của họ nốt.

- Cả 2 công việc cộng đồng trên đều phải công bằng, ai cũng có thể dễ dàng kiểm tra, xác nhận mức độ toàn vẹn của dữ liệu, nhưng sẽ là vô cùng khó khăn đối với những kẻ phá hoại (Because of Insider Fraud).

> Finally, I bring You: Consensus Protocol!

### Proof of Work - Bổ sung hoàn hảo

Mật mã học tiếp tục được ứng dụng vào kiến trúc của blockchain, lần này cũng ko xa lạ: [Hashcash của Adam Back](https://en.wikipedia.org/wiki/Hashcash).

Hãy nhớ lại phát minh Tiền Vỏ Sò ở bài viết trước, đó là một hệ thống Proof-of-Work cổ xưa. Tiền Vỏ Sò là bằng chứng của lao động, nó xác nhận giá trị tương đương với thời gian + công sức của việc mài dũa, chế tác. Hashcash cũng là một hệ thống như vậy, nguyên mẫu của Hashcash là một hệ thống xác nhận dựa trên bằng chứng công việc.

**Hashcash? Lại là "Hash" gì đó?**

Đúng. Hashcash cũng là một phương pháp băm (Hash) như giới thiệu ở trên, nhưng nó yêu cầu một người dùng muốn có được mã Hash đúng chuẩn "Hashcash" thì phải đoán mò. Haha.

Khi bạn muốn Mã hóa một password, một giao dịch hay một email nào đó, bạn thường chỉ cần 1 cú click chuột, hoặc enter một câu lệnh, máy tính của bạn sẽ tính toán cho bạn mã Hash đó trong vòng vài micro-giây. Nhưng với Hashcash, loại mã Hash đó giờ đây cần phải "Đẹp" nữa.

Đẹp ở đây, là mã Hash đó phải được tính toán hên xui một chút. Bạn thêm vào phần cuối của dữ liệu cần Hash một con số, Hash cả dữ liệu và con số đó. Mã Hash sinh ra nếu có 2 con số zero ở đầu, thì được coi là đạt chuẩn, ví dụ: "00th1s1s4n3x4mpl3h4sh". Còn nếu ko đạt chuẩn, bạn đổi con số kia đi, và tính Hash tiếp, mò tiếp, cho tới khi nào đạt 2 số zero ở đầu Mã.

**Rồi ai là người tính toán Hashcash?**

Giả sử trong Blockchain network đang có 1 Trang dữ liệu mới cần được xác nhận và update vào Sổ cái chung. 

Bất kỳ ai tham gia Blockchain/Bitcoin network đều được thông báo về Trang dữ liệu mới và lời mời "Xác nhận giúp" Trang dữ liệu này, bằng cách tính toán Hash-đẹp cho nó.

Người đầu tiên tìm ra được Hash-đẹp cho Trang dữ liệu trên sẽ thông báo trên toàn mạng: "Hey tao tìm được Block Hash cho Trang mới rồi".

Mọi người trong mạng sẽ kiểm tra nội dung Trang ghi chép mới (new Block) một lần nữa, xác nhận là nội dung hợp lệ và Mã Hash đẹp, rồi update Sổ cái (chain-of-blocks) theo người-tìm-ra-block đó.

### Nếu tôi định gian lận, thì sao?

Ví dụ như cuốn sổ của blockchain hiện tại đã ghi được 99 Blocks, bạn muốn gian lận bằng cách cố tình chỉnh sửa Block số 7, thì bạn phải vượt qua 2 bước xác nhận của blockchain.

1. Tính toán lại Block Hash cho Block số 7, sao cho phù hợp với Dữ liệu mới thay đổi trong Block 7.

2. Vì tính chất toàn vẹn của Blockchain, nên bạn bắt buộc phải tính toán lại toàn bộ Block Hash đi kèm sau nó, từ 8 đến 99.

**Tôi sẽ bỏ qua tất cả Block từ 8 đến 98, chỉ gắn Block 99 vào sau Block 7 thì có được ko?**

Blockchain-network luôn luôn coi cuốn sổ dài nhất (Longest Ledger) là sổ hợp lệ. Và vì tính đồng bộ hóa của nó nên nó chỉ chấp nhận một bản đúng duy nhất, các cuốn sổ khác ngắn hơn đều ko được chấp nhận. Như vậy, cuốn sổ của bạn sẽ bị loại bỏ nếu như nó ko phải là dài nhất.

**À thế thì nếu tôi ráng tính toán Block Hash cho 99 Block, chắc là vẫn khả thi chứ?**

Bạn có thể tham khảo những tính toán chi tiết của Satoshi trong Chapter 11, [Bitcoin white paper](https://bitcoin.org/bitcoin.pdf), gần như là bất khả thi.

Ngoài ra, tiêu chuẩn "đẹp" của Blockchain hơi khác Hashcash, tiêu chuẩn này thay đổi liên tục, thường tỉ lệ thuận với lượng người tham gia. Lấy Bitcoin làm ví dụ, hiện tại Bitcoin-network đã ghi được hơn 500.000 Blocks vào Sổ cái, và với tiêu chuẩn hiện nay của Bitcoin, việc tìm Hash-đẹp cho Block mới nhất sẽ tiêu tốn khoảng 60.000 năm của 1 con máy tính cá nhân đời 2018.

---

## Kết bài

Kết thúc bài thứ 2 về Blockchain, có lẽ ko ít thì nhiều, bạn có thể hiểu sơ về cách mà Blockchain/Bitcoin hoạt động, các công nghệ ẩn dưới nó.

Có thể bạn đã hiểu 100% và muốn đào sâu hơn.

Có thể bạn hoài nghi và cho rằng "Lý thuyết suông" là vô nghĩa.

Cũng có thể, bạn vẫn cảm thấy Blockchain phức tạp.

Dù lí do là gì, những bài viết tiếp theo sẽ là một trải nghiệm thực tế, để chứng mình rằng Blockchain thật sự ko phải là thứ gì đó bí ẩn, đáng sợ, phức tạp. Và bất kỳ Lờ tờ vờ nào cũng có thể tạo ra một "blockchain" đơn giản.

## References

https://bitcoin.org/bitcoin.pdf

https://en.wikipedia.org/wiki/Hashcash

https://en.wikipedia.org/wiki/SHA-2

https://www.ibm.com/blogs/cloud-computing/2017/04/11/characteristics-blockchain/
