---
layout: post
title: "Chapter 03: Chasing the Shark"
comments: true
description: "Nghệ thuật hắc ám - Phần 03: Thám Tử Cá Mập"
keywords: "haskell, pure, functional, hijack, game, server, wireshark, tcp, packet, filter"
---

# Những suy đoán ban đầu

Sau khi rage quit tập 2, tôi đã rất quyết tâm nghỉ game. Nhưng trước khi nghỉ, tôi đã mường tượng được việc mà đại ca minhchau bug.

Đặt cược nhiều hơn 2000 Xu, theo tôi đoán, là do team dev chỉ kiểm tra số xu cược 1 lần duy nhất bằng Client (tức là bằng cái app game được cài trên máy) và không kiểm tra lại lúc nhận thông tin ở Server. Ở đây các bạn cần hiểu là Game Online lúc nào cũng bao gồm 2 phần: Client - Server, nếu tập trung mọi xử lý ở Server thì sẽ làm cho server chịu tải lớn, cả về Sức mạnh xử lý lẫn băng thông. Ngược lại nếu phân tán xử lý ra cho Client thì rất dễ bị cheat.

Tiếp tục, như vậy tôi đoán tiếp cách để tận dụng bug này, có 2 hướng như sau.

* Mod lại client, chỉnh code để cho phép người dùng cược số xu lớn hơn 2000.

* Dùng tool của bên thứ ba (ko phải là client), giả danh Client và cược số xu lớn hơn 2000.

Tôi thiên về giả thiết 2, vì như giang hồ đồn thì bọn hắn chạy rất nhiều clone, và cược xu hàng loạt có khi lên đến 500.000 Xu 1 trận. Nếu Mod Client, thì công sức để cài và để chạy đồng loạt đúng giờ quá lớn, vài người ko đảm đương nổi.

---

# Lần trở lại thứ hai

Tôi nghỉ được 1 thời gian ngắn, tạm quên mọi thứ, thì khoảng 2 tháng sau nhận được tin nhắn của Rin. Đại loại là có 1 thằng nào đó chôm source và mở server lậu. Và tôi quyết định dùng server lậu này để hiện thực hóa những ý tưởng của mình.

Thật ra ở giai đoạn 2 (lần quay trở lại đầu tiên) thì tôi đã muốn kiểm chứng những suy đoán của mình. Rất tiếc, thời điểm đó tôi khá lười biếng, thiếu quyết tâm nên ko thực hiện.

Tôi bắt đầu chơi ở server lậu, và tạo nhóm chat riêng với Hanso4, Rin và Cherry (thím này về sau là Mod của Game X :D)

Lúc này là cuối tháng 06-2017. Rất may mắn, đây là thời gian vàng để tập tọe thứ gì đó. Tôi lúc đó mới học đến Week 06 của khóa CIS-194 và đang hăng máu chuẩn bị đề tài cho Final Assignment. Nên tôi chọn luôn cái ý tưởng mơ hồ của mình để làm Final Assignment, tức là tôi sẽ dùng Haskell để cheat Game X!

Dựa trên những suy đoán ban đầu, tôi đã chọn cách tiếp cận thứ 2, viết một tool mạo danh Client thực hiện công việc tà đạo haha.

Tôi có 2 lý do để chọn cách tiếp cận thứ 2: Một là tôi ko có kinh nghiệm modding app, Haskell sẽ ko áp dụng được vào phương án này, Java thì tôi đã chán ngấy và rất lâu ko đụng đến. Hai là viết 1 tool giả danh tuy tôi cũng ko có kinh nghiệm nốt nhưng tôi có 1 số kiến thức có thể áp dụng được (Client-Server model, Haskell, network package, network tracking)

---

# Let the hack begin !!!!

Trước hết, tôi tìm hiểu sơ qua về cách hoạt động của Game Server, mất 1-2 ngày. Cơ bản mô hình Game Server cũ sẽ dùng giao thức Tcp hoặc Udp để làm kênh giao tiếp giữa Client và Server. Tùy theo thể loại game mà chọn giao thức phù hợp, Tcp nếu bạn muốn đảm bảo toàn vẹn dữ liệu, Udp dành cho thể loại yêu cầu tốc độ cập nhật. Ngoài ra các game mới còn sử dụng Http (tôi cũng k hiểu lý do lắm).

Tiếp, đến tiết mục nghiền ngẫm dòng chảy dữ liệu, tôi có chút kinh nghiệm với Wireshark - thứ công cụ cực kỳ mạnh mẽ.

Okay, cài đặt Nox và Wireshark xong xuôi, mở game lên bằng Nox, sau đó ngay lập tức bật chế độ tracking netwwork của Wireshark. Tiếp đó quay lại Nox, login vào game, chờ màn hình loading chạy hết thì tắt chế độ tracking của Wireshark. Đây là kỹ năng tôi học được từ thời còn là sinh viên :v

Wireshark sẽ hiển thị như ảnh:

![Wireshark capture](/assets/images/aspect-of-programming/wireshark.png)

Tôi chú ý đến 2 packet là 19 và 31, đây là 2 dòng POST request, được gửi đến 1 domain rất quen thuộc "Gaba", hehe Gaba là platform để login và nạp tiền của Game X. Tất nhiên tôi phải căng mắt sàng lọc cả tiếng mới tìm được, chứ ko thần thánh gì :). 

Tiếp tục view chi tiết 2 cái request trên: Checkuser (19) và GetUser (31), nội dung POST của nó lần lượt là:

> partnerId=0&userName=hoason103&deviceId=d80f998b16396187&serverMode=UNKNOWN&password=ahihi123&refcode=0&gameId=46

> session=faa6f650-b966-4eb6-b1f4-9fe9028e8d16&serverMode=UNKNOWN&hash=f0ed1769de065b7ee318b647c92ed6a6&time=1523809261967

Ahha, tôi tập trung vào cái packet 19 hơn, vì nó chứa thông tin đăng nhập mà tôi vừa gửi :). Chưa vội làm gì, tôi copy request-response và lưu lại vào 1 file text, tiếp tục xem Wireshark.

Tôi tiếp tục để ý tới cái POST request 55, host lại rất rất quen thuộc, lần này là sub-domain khác (api.kd).

![Wireshark capture](/assets/images/aspect-of-programming/wireshark2.png)

View chi tiết (follow TCP thì Wireshark sẽ hiện response đã được decode)

![Wireshark capture](/assets/images/aspect-of-programming/wireshark3.png)

Ồ có vẻ như ở request 55 này, Client đang dùng thông tin từ 2 request 19 và 31 để gửi thông tin đến 1 sub-domain khác của Gaba. Response là list danh sách máy chủ, tuyệt vời. Tôi cũng lưu lại request-response số 55 này.

Quay lại với wireshark, tôi filter packets theo ip 123.31.25.75. IP này tôi lấy từ list server trả về từ request 55 ở trên, đây là địa chỉ của server 101 (là server tôi vừa login bên Nox). Kết quả là 1 loạt giao tiếp bằng TCP của máy tôi tới 123.31.25.75. Wow, that's enough. Note là có 2 gói tin được gửi từ máy tôi lên server như sau:

> T...P.LOGIN 0.0.1 10 101 1256313440 123 1523809263 d514402770a4a253e659f373b89c8f94 0

> ......ENTER 1256313440 101001099.

2 thông tin gửi đi này là đã được wireshark decode ra ASCII, gói tin gốc là 1 dãy số thập lục phân (Hex)

Đoạn này viết vậy thôi, chứ mất vài lần login và cả buổi tối để nghiền ngẫm, lọc và test.

---

# Kết luận đầu tiên

Dựa vào những gì thu được từ Wireshark, tôi đưa ra kết luận của mình, tất nhiên chưa được kiểm chứng.

* Có 1 Server HTTP để chứng thực đăng nhập, sau đó trả về 1 số thông tin cần thiết như session, token, time , server info, bla bla...

* Sau đó Client sẽ dùng thông tin ở HTTP response trên để kết nối với Game Server qua giao thức TCP.




