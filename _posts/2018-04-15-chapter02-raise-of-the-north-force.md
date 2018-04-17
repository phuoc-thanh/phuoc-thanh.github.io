---
layout: post
title: "Chapter 02: Raise of the North Force"
comments: true
description: "Nghệ thuật hắc ám - Phần 02: Thế lực phương Bắc"
keywords: "haskell, pure, functional, hijack, game, server, tool, programming"
---

# Thủ công vs Công nghiệp

Bất kỳ ngành nghề nào, khi mở rộng từ thủ công đến công nghiệp đều là 1 sự nhảy vọt, và yếu tố "Tự động" và "Máy móc" là phần thiết yếu nhất, đương nhiên.

Quay lại vào thời điểm giữa 2016, lúc tôi nghỉ game và ku Chinh (or Chính maybe) đang phát triển việc làm ăn của hắn. Ku này ở Nha Trang, chơi game tay ngang thôi.

**Vấn đề đầu tiên**

Là nhu cầu đang lớn dần. Khi bán 10k Xu với giá 100k, nếu 2-3 người mua nhỏ lẻ thì vẫn OK, có nghĩa là hắn cần lận lưng 10-15 acc Vip3. Hắn có thể dạo quanh vài vòng các server để xin acc, và nạp thêm (50k/1acc Vip3), vẫn đáp ứng đủ. Nhưng khi có 5 khách hàng mua 50k Xu, thì cần có 25acc Vip3, chà con số bắt đầu nở. 10 khách hàng? e là hắn ko chịu nổi.

**Vấn đề thứ hai**

Là tay. Đúng vậy, cần tay để bấm. Giả như một kỳ liên chiến hắn có 10 khách hàng, chia làm 3 vòng top32, top16, top8. Mỗi vòng 3 khách, cần bấm 15+3 là 18 acc.

Máy Core i5 chạy được 4 acc, thì phải là 4 máy + 2 điện thoại. Liệu có bấm kịp? Maybe, I just don't know.

Thêm một điểm cần lưu ý nữa là phải có tay để chơi những acc clone (Vip3) sao cho mỗi acc kiếm đủ 2k xu 1 tuần, không khó lắm nhưng mất thời gian.

**Vấn đề thứ ba**

Là chọn kèo. Hehe, nếu hắn muốn bán xu, phải chọn kèo thật chắc ăn, nếu kết quả ngược lại, thì acc cùi Vip3 sẽ ăn xu acc chính. Thế nên hắn có 2 con đường, nương nhờ kèo người khác và phó mặc số phận, hai là phải nuôi acc/ mua acc khủng thường xuyên vào liên chiến để có thể dàn xếp tỉ số - bán độ. Vậy nhưng cần bao nhiêu acc cho đủ? vấn đề khá nan giải.

**Kết quả**

Quả thật khó. Nhưng hắn có thể từ chối bớt kèo, thu nhập ít đi, hoặc có thể chiêu mộ thêm đệ để cày. Thời gian đó tôi ít theo dõi, chỉ biết là một vài tháng sau đó, hắn trốn biệt, ôm theo một khoản nợ. Vì cơ bản để mà mua được xu, người chơi phải tin tưởng hắn, chuyển tiền trước và giao acc chính cho hắn.

---

# Lần trở lại thứ nhất

Tôi nghỉ một thời gian khoảng 6 tháng, quay trở lại vào khoảng tháng 10-2016 (ko chính xác lắm, nhớ vậy thôi). Lần này tôi đầu tư đánh Sơ Cấp, vì ít tốn kém nhất.

Qua vài kỳ liên chiến, tôi nhận thấy một nhân vật tên là "ngocpck", hắn rất mạnh ở Sơ cấp. Ngocpck ở sv66, sv cũ của tôi, sơ qua lúc còn chung server 66 thì ngocpck là tay biết chơi, kì cựu, biết ép level dưới 59 để đánh, biết đi boss, biết bật top tiêu v.v... 

Phong thanh trên group thì té ra ngocpck chính là một vị vua không ngai, hắn chỉ chịu nhượng bộ những anh vip quá cao (vip13 trở lên), xu của hắn ko biết bao nhiêu nhưng vung tay cực kì bạo, ăn top liên tục để liên chiến. Ngoài ra hắn còn là đầu nậu bán xu. Giá rẻ 1/2 so với ku Chinh, tức là 1m = 20 vạn, 500k = 10 vạn (100.000 Xu). Và không bán lẻ tẻ.

Wow, quá lợi hại, vừa mạnh, vừa bán xu, vừa nuôi acc.
---

# Thế lực phương Bắc.

Mục tiêu của tôi sau vài tháng là vào chung kết liên chiến Sơ cấp, thời kì này, ngoài ngocpck có 1 số nhân vật nổi trội ở Sơ cấp:

* 50CM: ku này đầu tư cùng lúc với tôi, và đầu tư mạnh hơn tôi rất nhiều, biết chơi.

* Hanso4: ku này lão làng trong game, biết mọi ngóc ngách, tính năng, chỉ số, chơi từ thời sơ khai, biết cách tự tạo acc Vip3 và chuyển xu kiểu thủ công như "Chinh" đại hiệp. Hắn đầu tư vài chục acc Vip3 để ăn xu hằng tuần.

* Rin: đại ca này lớn tuổi hơn tôi, rất đam mê game này, có thể thao thao bất tuyệt cả ngày về chiêu số, đội hình, chỉ số công thủ tốc, v.v....

* JameRoyal: ku này là đệ của ngocpck, chuyên đứng ra nhận kèo mua-bán xu với các đại hiệp khác, sau đó sẽ đá lại cho ngocpck làm kèo.

Trong số những tay hảo thủ ở trên, ngoại trừ Hanso4 tự lực cánh sinh ra, còn lại hoặc là nạp, hoặc là mua Xu, chỉ có JameRoyal và ngocpck là ngon vì 2 đứa này bán xu. Tôi thuộc thành phần vừa nạp vừa mua.

Để mua đc Xu thì cũng phải tham gia Group và tìm đến ng bán, vâng, và lúc này sự thật được hé mở. Ở Game X này, chỉ có 1 hội bán xu duy nhất, hội của ngocpck và Jame, ngoài ra còn có minhchau (sv71), lão béo, lão hạc cùng sv6 và 1 số acc top trong liên chiến. Có thể nói, hội này thầu gần hết các acc top liên chiến, bán xu số lượng lớn (bao nhiêu cũng có), thao túng toàn bộ Game. Toàn bộ thành viên nhóm này đều ở Hanoi...

---

# Phân tích kỹ thuật.

Như tôi kể trên, cả hội thao túng Game tới mức gần như tuyệt đối, chỉ chịu thua Vip12-13 trở lên, và làm ăn chuyên nghiệp.

Vừa tìm kiếm thông tin, vừa thảo luận với game thủ khác như Rin, Hanso4, 50cm, vừa trực tiếp mua xu từ Jame, tôi có được những kết luận sau:

* Có một bug quan trọng trong game: Đặt cược tối đa vượt quá 2000 Xu, nhưng lỗi này ko biết tại sao chỉ có hội ae phương Bắc kia làm được. Điều này ảnh hưởng rất lớn, vì nếu đặt cược càng lớn, thì càng chắc chắn. Khi đặt 10k-20k Xu thì ko lo những kẻ "ăn ké" (me sát giờ, chọn đúng kèo và easy money -)) vì tỷ lệ chia % lớn hơn nhiều. Thứ 2 là clone vip3 cũng có thể đặt lớn như vậy thì không cần tới nhiều clone, thay vì 5acc mỗi acc 2k, giờ đây đây chỉ cần 1-2 acc là đủ để cược được số xu tương đương.

* Nhân vật cao cấp: minhchau - sv71, đây là người khai thác được bug game trên, và chỉ một mình đại ca này làm được, ngocpck hay Jame là những tay nuôi clone, nhận kèo bán xu, xếp kèo bán độ mà thôi.

* Thông tin bên lề: Hanso4 và Rin quả quyết rằng minhchau không dùng cách thủ công, mà lão đang dùng 1 thể loại tool nào đó để khai thác bug trên, Hanso4 có ý định mua tool nhưng ko có kết quả. Rin thì cho rằng ngocpck và hội của hắn đang giữ tầm 300-500 acc clone vip3, 1 con số khổng lồ.

---

# Quitter tập 2.

Tôi vẫn chinh chiến vài tháng sau đó, đến khoảng tháng 3 hay 4-2017 gì đó thì tôi quit. Tôi quit vì được biết 1 thông tin độc đáo: A-e ngocpck đã tìm được bug mới: Lấy bạc không giới hạn.

Như tôi có nói ở phần 01, bạc không thể mua được gì giá trị, nhưng đối với số bạc quá lớn, phải nói là vô tận, thì bạc lại cực kỳ hữu ích. Nhân vật sau khi đập đá bằng bạc vào 1 số thứ thì trở nên mạnh mẽ điên cuồng.

Tôi lờ mờ nhận ra vài thứ và quyết định Quit.

![Bạc đầy kho](/assets/images/aspect-of-programming/silver_money.png)

Đây là hình ảnh bạc tràn kho.