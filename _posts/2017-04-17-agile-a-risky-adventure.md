---
layout: post
title: "Agile - Một chuyến phiêu lưu đầy rủi ro"
comments: true
description: "Agile - Một chuyến phiêu lưu đầy rủi ro"
keywords: "agile, scrum, disease, evil, methodology"
---

### [Tổng hợp, biên dịch từ nhiều nguồn, có diễn giải theo ý kiến riêng]

# Agile - Một chuyến phiêu lưu đầy rủi ro

Cho tới nay, 2017. Agile nói chung (bao gồm cả Scrum) đã trở thành 1 loại tôn giáo trong ngành phần mềm, nhưng theo cá nhân tôi, Agile là 1 loại bệnh truyền nhiễm. Và những "chiên gia" (Consultant) về qui trình đang bán cho khách hàng 1 loại thuốc an thần liều mạnh nhưng ẩn chứa đầy rủi ro - Agile...

Tập đoàn đa quốc gia với mọi thứ đang trong khuôn khổ vận hành trơn tru bỗng 1 ngày đòi đổi mới với qui trình "Agile".  
Công ty lớn, trung bình sau khi quá mệt mỏi với CMMI đã được 1 vài anh gạo cội rỉ tai về "Scrum".  
Nhóm khởi nghiệp năng động, đầy hoài bão, tất nhiên không thể bỏ qua "Agile" hay XP Programming.  
Khách hàng cấp tiến, trong buổi hợp mời thầu, cũng hỏi cả nhà thầu: "Anh nghĩ như thế nào về Agile vs Traditional".  

Và những nơi đang áp dụng Agile vào quá trình sản xuất phần mềm, thật sự những con người ở đó đang tham gia vào 1 chuyến phiêu lưu đầy rủi ro.  

![Agile Risky Adventure](/assets/images/agile-risk.jpg)

## Agile, Scrum là gì?

Về định nghĩa Agile, Scrum, có lẽ thông tin đã tràn mọi ngõ ngách internet ròi. Nhưng cũng nên ngó lại tuyên ngôn và 12 nguyên tắc
của Agile 1 xíu để có thể nói sâu ở phần tiếp theo của câu chuyện.
Xin mời xem qua:

http://agilemanifesto.org.


## Agile và 12 tuyên ngôn (Agile Manifesto) - The hype of common sense
Đoạn này xin mượn 1 vài ý của Luke Halliwell - 1 Game Developer "chân chính", link bài gốc ở phần tham khảo cuối bài.

1. Individuals and interactions over processes and tools
Vâng, dĩ nhiên con người và sự tương tác là thứ quan trọng hơn. Nhưng ngạc nhiên chưa, Agile hoàn toàn nói về qui trình, và cách áp dụng nó, hiếm khi nào Agile nhắc tới yếu tố con người mới chính là quan trọng nhất trong 1 dự án. 

2. Working software over comprehensive documentation
Điểm này khá là đặc thù cho từng mảng nhỏ bên trong ngành phần mềm. Như Luke nói thì công việc của anh ta chẳng có nhiều tài liệu để nhúng tay vào, như vậy điểm này khá là vô ích, hơn nữa nó sẽ khuyến khích dân chúng bỏ bê việc tài liệu, việc đó thì hơi đáng sợ hehe.  
Ngoài ra, trong mảng Software service, Maintenance, Support, Security, Cloud-based service... thì Document là cực kỳ quan trọng đối với khách hàng. Cá nhân tôi đã làm những task 40h nhưng chỉ 8h là dev, và 32h còn lại chỉ để documenting... So what?
Như vậy, cơ bản nó ko mang lại lợi ích gì nhiều.

3. Customer collaboration over contract negotiation
Okay, đồng ý nhưng như trên, trong 1 số trường hợp, nó không mang lại lợi ích thực sự.
Kinh nghiệm cá nhân thì cái việc "Customer collaboration" thực sự là 1 thảm họa của dev. Đôi khi 1 task đơn giản, bạn phải bỏ tận 6h chỉ để get confirm từ customer, sau đó dev 2h. Vui vẻ.  
Chưa kể là khi được đà custom, change mà ko có evidence, contract, aggrement thì cực kỳ rủi ro và nó xảy ra cũng thường xuyên lắm :))

4. Responding to change over following a plan
Thứ nhứt, tôi xin cam đoan là ko có 1 thợ code nào khoái sự thay đổi từ khách hàng cả.
Thứ hai, làm việc mà ko có 1 kế hoạch, nghe có mùi mù quáng, giống như lái xe từ quê lên Saigon chơi mà ko cần bản đồ vậy =)) 

## Hyping common sense

Triết lý của Agile (Agile Manifesto) nghe rất hay và hấp dẫn, dĩ nhiên cả với 12 nguyên lý của Agile nữa.
Nhưng điều mà nhiều anti muốn nói là tất cả những điều này đều là "Common Sense", tức là những lẽ thường, dễ dàng nhận thấy, nếu bạn đủ thông minh.

Và triết lý Agile chỉ cường điệu hóa những điều đó mà thôi. Chúng ta đều biết nó đúng, hay, và bổ ích. Nhưng làm thế nào?

Câu chuyện đc mang sang Scrum, khi đó triết lý Agile mới được áp dụng thành vào 1 dự án, 1 team.

Có rất nhiều ý kiến phản đối và bổ sung thêm cho 12 nguyên lý của Agile, các bạn có thể tham khảo link dưới bài. Nhưng chỉ cần bạn làm việc đủ lâu trong ngành phần mềm thì bạn sẽ thấy được thiếu sót của 12 nguyên lý này, nó chỉ đúng trong môi trường lý tưởng. Nghĩa là ko áp dụng được nhiều như ta nghĩ, ko phù hợp với đại đa số kiểu dự án...

Ví dụ 2 principles sau, hãy thật lòng với chính bạn, bạn có nghĩ nó tốt ko? riêng dev quèn như tôi, it's bullshit

> Business people and developers must work together daily throughout the project.

> Welcome changing requirements, even late in development


## Business-driven engineering


> High-talent people is more important and success than micro - managed team & processes

Theo Michael, trong ngành Software Engineering, tồn tại 2 thể loại công ty: Business-driven và Engineering-driven.

Khi công ty được điều hành bởi kỹ sư, sẽ rất khó khăn và nhiều thách thức, điều đó ko phải lúc nào cũng tốt. Nhưng trong môi trường đó, nơi mà vai trò của kỹ sư được đề cao và tin tưởng. Sản phẩm, công việc anh ấy hoàn thành được tôn trọng và công nhận. Và ai cũng sẽ happy với task/job của mình. Như vậy cty có khả năng lớn sản sinh ra những sản phẩm chất lượng cao (Yếu tố con người)

Ok, còn với công ty dạng Business-driven thì sao? Ổn thôi, theo Michael, thì trong trường hợp này bạn nên tìm đến contractors, tuyển lính đánh thuê theo job, và đó là lựa chọn tốt nhất nếu bạn muốn có những kỹ sư chất lượng cao. Vì những kỹ sư tài năng đã chọn những công ty engineering-driven mất rồi.

Và rất tiếc Scrum (Agile implemented) thường hướng công ty theo con đường Business-driven, nơi mà lời nói của khách hàng là tối thượng, dev ko có quyền lực và được setup để vào the-same-team-of-low-lvel, tức là 1 đội ko có thứ hạng, kỹ năng của người trong đội được coi là như nhau. Chi tiết công việc hằng ngày dev làm sẽ phải giải trình với Scrum master (the big scam of Scrum) hay Product Owner, 1 dạng qui trình micro-managed mà ko dev nào muốn bị áp đặt cộng thêm 1 loại non-technical manager ko dev nào muốn dưới quyền.

## Agile sẽ gây tổn hại đến career path của 1 Developer 
Đoạn này xin lấy ý chính từ blog của Michael O Church 

> Instead of working on actual, long-term projects that a person could get excited about, they’re relegated to working on atomized, feature-level “user stories” and often disallowed to work on improvements that can’t be related to short-term, immediate business needs (often delivered from on-high)

Đúng vậy, Violent transparency, 1 loại văn hóa của Agile/Scrum sẽ khiến bạn thay vì theo đuổi những dự án dài hạn, bỏ hết tâm và sức mình vào những gì bạn hứng thú để đảm nhận 1 loại công việc ngắn hạn, nhàm chán.  

Khi bước vào tuổi chín của sự nghiệp (khoảng 30), bạn - 1 kỹ sư phần mềm, mong muốn mình có thể gánh vác những công việc tầm cỡ về hạ tầng hệ thống, kiến trúc, nghiên cứu, và khả năng lãnh đạo. Trong khi với Agile/Scrum, ngày qua ngày bạn được giao những công việc ngắn hạn theo "User story" (khoảng 2 tuần), và những công việc này theo như Michael nói, chính là "grunt work".  

Grunt, làm tôi nhớ tới con orc cầm búa trong Warcraft 3, grunt orc chỉ biết cầm búa và lao vào đối thủ, không có 1 kỹ năng nhạy bén nào =)). Và grunt work - chính là loại công việc mà 1 anh grunt đảm nhận. Những feature tẻ nhạt, lặp đi lặp lại, ngắn hạn, thiếu sáng tạo để đáp ứng ngay cho nhu cầu cấp thiết của Client.  

## Khi nào nên áp dụng Scrum?

Scrum dành cho những dự án đột xuất, khẩn cấp và yêu cầu hàng đầu là delivery, tức là phải xong việc thật nhanh.  

Khi nhận dự án kiểu này, cty sẽ lập 1 team với những chiến binh có kinh nghiệm: Dev nhanh, chịu OT, có trách nhiệm cao, ko phàn nàn với sự thay đổi liên tục từ khách hàng.

Team sẽ có 1 Leader, hoặc Executive có lẽ tốt hơn -> xin gọi tắt là Osin. Trách nhiệm chính của Osin là làm cầu nối giữa client và dev team. Công việc chủ yếu của Osin:  

1. Lắng nghe yêu cầu/thay đổi của khách hàng (User Story) và dịch ra thành technical-task cho dev team.
2. Giải thích technical thing sao cho dễ nghe với khách hàng và giúp họ lựa chọn giải pháp kỹ thuật.
3. Dựa trên estimation của team (hoặc member) để deal với khách hàng về tgian hoàn thành.
4. Overview toàn bộ mọi thứ team đang làm để đảm bảo "all jobs will be done"!  

Hãy luôn ghi nhớ rằng những dự án này là "short-term", tham gia quá nhiều dự án đột xuất dạng này sẽ ảnh hưởng lớn đến sự phát triển của 1 kỹ sư chuyên nghiệp. Bởi vậy có 1 số điểm cần lưu ý khi thực hiện:

1. Nó chỉ nên xảy ra 1 hoặc 2 lần trong năm cho mỗi cá nhân tham gia.
2. Trong tgian diễn ra, mọi ng phải thống nhất rõ ràng trước là ko đánh giá hiệu suất cá nhân mà chỉ tập trung vào nhiệm vụ.
3. Giảm tối thiểu Micro-manage, 1 điều ko tránh khỏi đối với Agile

Micro-manage là vấn đề thường xuyên gặp trong các môi trường khác kể cả ngoài Agile và ngoài lĩnh vực Software. Điểm này sẽ làm những chiến binh của ta khó chịu và giảm hiệu quả khi bị giám sát/theo dõi. Có lẽ nên viết thêm 1 phần khác về Micro manage

### Hoàn cảnh áp dụng

Cũng theo Michael O.C, có 2 hoàn cảnh thường xảy ra:
* Khi 1 cty áp dụng Rapid Development quá nhiều cho 1 cá nhân thì chắc chắn có gì đó sai sót vì những dự án gấp gáp kiểu này có vẻ khá hiếm hoi.

* Cty đang gặp vấn đề với quản lý Client Relationship khiến cho toàn bộ dự án/tasks đều trong tình trạng đột xuất, gấp gáp.  

Okie, cả 2 điểm này tôi đều gặp. Khi cty bạn đang làm việc với khách hàng là Digital Marketing Agency, những dự án xoay quanh quy mô của 1 campaign, luôn luôn bị hối thúc. Bản chất của nó chính là "Rapid", "Short-term", "Deliver First" nên toàn bộ team đều phải chạy theo 1 kiểu làm việc hỗn loạn như trên... 

### Anti

Những kiểu dự án như sau là thể loại ko nên áp dụng Agile/Scrum:

* Dự án có độ phức tạp lớn, về mặt technical có nhiều vấn đề cần giải quyết và cần thời gian dài (ko thể xác định hay ước lượng rõ ràng) để giải quyết. Khi đó rất khó để đưa giải thích hoặc deliver thường xuyên cho khách hàng.

* Dự án về Game, tương tự như trên. Bạn ko thể giao 1 phần gì đó để khách hàng có thể xem xét và chỉnh sửa đc.

* Những dự án sáng tạo

## References
https://michaelochurch.wordpress.com/2015/06/06/why-agile-and-especially-scrum-are-terrible/

https://lukehalliwell.wordpress.com/2008/11/16/the-agile-disease/

https://www.quora.com/Why-do-some-developers-at-strong-companies-like-Google-consider-Agile-development-to-be-nonsense
