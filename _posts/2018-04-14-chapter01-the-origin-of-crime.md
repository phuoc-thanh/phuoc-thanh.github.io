---
layout: post
title: "Chapter 01: The Origin of Crime"
comments: true
description: "Nghệ thuật hắc ám - Phần 01: Khơi nguồn tội ác"
keywords: "haskell, pure, functional, hijack, game, server, programming"
---


# Quá khứ bỏ quên

Thế hệ 8x, các bạn chắc không quên cơn bão Game Online 2004-2005-2006 nhỉ, cái thời ADSL mới được nhân rộng, tôi cũng là một con thiêu thân lao vào thử lửa. 2004, năm đó tôi học lớp 10, bắt đầu bằng MU Hanoi. Internet thời MU Hanoi tạo nhân vật hết 15p, vào game hết 10p và mở rương đồ hết 15p. Fuck, nếu là các bạn trẻ bây giờ, có khi đã đập bể vài bộ chuột phím rồi ấy :). Phải công nhận Game Online thời đó như là ma thuật, khiến ngta nhìn vào màn hình quên ăn quên ngủ, kiên nhẫn chỉ để thấy nhân vật mình đi lại và chém vài nhát.

Sau đó là Gunbound, Line Age 2, Dota... và tôi thi vào ngành CNTT, tôi nghĩ sau này mình sẽ sản xuất game.

Vâng tôi biết chắc rất rất nhiều anh/chị/em dev hiện tại, lao đầu vào ngành CNTT chỉ vì thích máy tính, thích chơi game.

Tôi vẫn chơi game, cho tới lúc ra trường... dòng đời đẩy đưa, tôi làm Web Server (Java), bỏ quên lý tưởng Sx Game năm nào...

Nhờ những tiếp xúc rất sớm với Game Online và được học cơ bản về lập trình, tôi có chút hiểu biết về mô hình Game Online, cũng có thể gọi là Client-Server

Tháng 12-2015, lần đầu tiên tôi chơi 1 Game Online dành cho Mobile - gọi là Game X đi, lúc đó game mới mở được hơn 1 tháng, tôi vào server 21.

Khoảng tháng 4-2016, Game X mở tính năng liên chiến xuyên Server, tạm gọi là Đấu Trường Thú - gọi tên theo đam mê 1 thời của tôi Bloody Roar hehe -)).

Đấu Trường Thú mở được 1 tháng tôi nghỉ game, vì đánh nhau ko lại các anh đại gia top server. Hihi. Đây là trải nghiệm tiền đè chết người đầu tiên mà tôi gặp. Các game trước tôi chơi 1 là RPG cày cuốc, 2 là thể loại đối kháng yêu cầu kỹ năng như DoTA.

---

# Game X

Game X mà tôi kể trên, là dạng Turn-based Strategy. Mỗi trận đánh nhau là 20 lượt, thể thức 5 vs 5 (mỗi team 5 nhân vật). Các nhân vật được mô phỏng từ đại hiệp trong truyện chưởng Kim lão gia.

![Màn hình chính trong game](/assets/images/aspect-of-programming/in-game.png)

Cơ bản như hình trên thì 1 đội có 1 nhân vật chính và 4 tướng có thể đi kèm theo, trong ảnh là Tống Thanh Thư và Tiểu Long Nữ.

Tiền tệ trong game là Xu và Bạc, Bạc thì dễ kiếm bằng các hoạt động trong game, nhưng lại ko có giá trị mấy. Xu là tiền tệ chính để sắm đồ giúp nhân vật mạnh hơn.
Xu cũng có thể kiếm nhưng lại quá ít, mỗi ngày siêng năng cày cũng đc 200-400 Xu mà thôi. Xu cũng chính là công cụ để nhà phát hành (NPH) hút máu game thủ.

Giá nạp của Game X: 100.000 VND = 1000 Xu, nạp 1tr được 10k xu kèm khuyến mãi linh tinh thì coi như 1 củ khoai lang = 20k xu đi.

Vip15 (cao nhất) là phải nạp 100 củ khoai lang. Tính tới thời điểm tôi nghỉ game thì đã có khoảng 10-15 anh tài Vip15, chưa kể rất nhiều đại hiệp Vip13,Vip14. Thời điểm game tàn (cuối 2017) vẫn có 1 vị đại hiệp quăng vào 80 chai để bá chủ Đấu Trường Thú.

---

# Đấu Trường Thú

Nếu các bạn chơi game mobile nhiều thì sẽ nhận thất đa số game thẻ bài dạng này thường mở rất nhiều server, liên tục cỡ 1 tuần 2,3 cái - chủ yếu để hút máu mạnh hơn -)).

Vậy nên server mới sẽ là nơi thi đua nạp tiền, nhưng như vậy chưa đủ, cần tạo ra tranh đua hơn nữa để hút cả ở những server cũ. Thể là 2 tính năng mới ra đời: Gộp Server cũ và Mở liên chiến (Đấu trường Thú).

Đấu trường này như Champion League vậy, nhưng có 3 cấp độ: Sơ cấp (cấp nhân vật 59 trở xuống), Trung cấp (lvl 60-89) và Cao cấp (lvl 90 trở lên)

**Vòng loại: Diễn ra vào chiều thứ 6**

Game thủ chỉ báo danh, việc sắp xếp bốc thăm, khiêu chiến, tính kết quả sẽ do Máy chủ liên chiến làm hết. khoảng 7PM tối thứ 6 là có kết quả.
Đánh loạn xà ngầu cùng cấp độ, trên toàn bộ server, thắng khoảng 6-7 trận thì vào vòng loại trực tiếp, cũng có trường hợp xui thắng 8 trận nhưng ko vào, hay hên: thắng 2 trận vào luôn.

Như vậy có 32 đấu thủ sẽ được chọn ra để vào vòng loại trực tiếp cho mỗi cấp độ.

**Vòng loại trực tiếp: Diễn ra vào tối thứ 7**

Sau khi vòng loại diễn ra thì Máy chủ liên chiến tiếp tục bốc thăm chia cặp để đánh top32, gồm 4 bảng A,B,C,D cho mỗi cấp độ Sơ, Trung, Cao.

Đây mới chính là nơi để game thủ thể hiện kĩ năng sắp xếp, chiến đấu. Vòng loại trực tiếp diễn ra vào 7PM đánh top32, 8PM đánh top16, 9PM đánh top8. Sau vòng loại top8 thì chỉ còn lại 4 game thủ vào bán kết.

**Vòng chung kết: Diễn ra vào tối chủ nhật**

Cũng với thể thức như vòng loại trực tiếp, bán kết diễn ra vào 7PM, chung kết diễn ra vào 9PM.

---

# Mức độ đẫm máu

Nếu chỉ là đánh nhau để xác định ngôi vương của toàn bộ server, thì có thể nói đại hiệp nào hào phóng hơn đương nhiên là người chiến thắng. Cuộc chơi trở thành nơi so tài của Vip14-15. Nhưng không, Đấu trường thú có một tính năng đặc biệt thú vị, gọi là "Đặt cược" (a.k.a betting haha)

Trước khi mỗi trận đấu ở Vòng loại trực tiếp/Vòng chung kết diễn ra, người chơi có thể cược đấu thủ chiến thắng. Bên thắng ăn hết Xu cược của bên thua.

Ví dụ, trong trận đấu của Lão Hạc vs 98 Giới (2 đại hiệp vip15 mạnh nhất thời đó). Tôi đặt 2k Xu cho Lão Hạc, bên 98 Giới có 2 đại ca khác đặt cược 2k mỗi người, tổng là 4k cho 98.

Nếu Lão Hạc win, tôi ăn toàn bộ 6k (2k cược và 4k thắng). Nếu 98 win, 2 đại ca kia mỗi người ăn 3k (2k cược và 1k được chia theo % từ tiền ăn được, ở đây là 50-50 vì mỗi người đều đặt 2k).

Số tiền cược tối đa cho 1 đấu thủ là 2k Xu, tối thiểu là 100 Xu (toàn bộ phải cược bằng Xu hết nhé, ko chơi bạc).

Chỉ những game thủ Vip3 trở lên mới được tham gia cược xu (nạp 50k là Vip3 nhé)

![Liên chiến](/assets/images/aspect-of-programming/cross-war.png)

Các bạn thấy đó, ở trên đầu mỗi đấu thủ chính là số xu cược.

---

# Manh múng lập cơ đồ

Khi tính năng liên chiến trôi qua được 2 kì, đã có 1 vị thiếu hiệp nổi lên, hắn đăng trên group (group fb, do NPH tạo để game thủ đàm đạo) là bán xu, rẻ hơn nạp. 100k = 10k xu, như vậy tương đương nạp 1 triệu (1 triệu nạp vào game được 10k xu + quà khuyến mãi).

Chà chà, tay trẻ tuổi này tôi quen, hắn tiết lộ:

> Bí quyết ở đây là thời gian, và 1 chút đầu tư. Giả dụ anh có 5 tài khoản (acc) Vip3, hãy chọn 1 kèo nào anh cảm thấy chắc chắn (chênh lệch lực chiến quá xa). Hạn cược xu và update đội hình sẽ sớm 5 phút so với thời điểm diễn ra trận đấu. Trận 7PM thì khóa cược xu lúc 6.55, tương tự là 7.55 và 8.55. Oh yeah, nếu anh nhanh tay đặt 5acc Vip3 đó cược vào bên thua, và dùng acc chính đặt vào bên thắng ngay thời điểm ít giây trước khi khóa, như 6.54.40 chẳng hạn, thì kết quả là easy ăn 10k Xu.

Đó là về mặt lý thuyết, vậy để thực hành thì ta cần 6 máy điện thoại, hoặc 2PC (mỗi PC chạy giả 3 giả lập) để thực hành.

Những kì liên chiến đầu, ku này làm ăn khá tốt. Nhưng đó cũng là thời điểm tôi quit, vì ko có khả năng chơi lại VIP cao.