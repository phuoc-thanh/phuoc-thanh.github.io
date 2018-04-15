---
layout: post
title: "Programming - Nghệ thuật hắc ám"
comments: true
description: "Programming - Nghệ thuật hắc ám"
keywords: "haskell, pure, functional, dark, power, hijack, beauty"
---


# This is crazy!

Có một câu nói mà tôi tâm đắc từ thời còn là sinh viên:

> Bạn chưa mất ngủ vì công việc tức là bạn chưa làm việc

Có thể trong cuộc đời code dạo, chúng ta có rất nhiều đêm mất ngủ, nhưng hàng tháng mất ngủ thì phải nói sao nhỉ? Đâu có mấy :)

Tôi chưa từng nghĩ mình sẽ làm được gì có ích, xài được bằng Haskell. Với Haskell, lúc bắt đầu học tôi chỉ nghĩ đó là một môn học. Nhưng cuối cùng ứng dụng đầu tiên của Haskell mà tôi làm được lại hơi mờ ám, tà đạo một chút xíu. Quyết định viết series này, nghĩ mình hơi khùng, nh cá tính tôi ít khi thay đổi quyết định.

Có thể nói chủ đề của series, vấn đề mà tôi giải quyết, có thể quá bé, quá ít để viết ra.

Có thể nói code mà tôi viết, chung qui là ko có gì đặc biệt, ai cũng làm được.

Có thể nói quá trình làm ra ứng dụng không có gì nổi trội, ko có bài học.

Uây, nhưng t ko quan tâm lắm, viết để ghi nhớ những lần chiến tranh bàn phím, những đêm bật dậy lúc 3h sáng để thực thi ý tưởng, những kinh nghiệm học được từ Haskell, hay đơn giản hơn: Viết để xả stress. Hihi.

"Nghệ thuật hắc ám" nghe có vẻ hoành tráng, thật ra ko tới mức cao siêu trừu tượng gì cho lắm, chỉ đơn giản nhớ tới truyện Harry Potter thoi hehe.

Tại sao hắc ám? Vì nói cho cùng, nó là khai thác lỗ hổng của một server và bug của ứng dụng.

---

# This is long!

Đây sẽ là series khá dài, bao gồm nhiều phần, và có cả source code. hãy sẵn sàng.

Series dự tính:

[Chapter 1: The Origin of Crime - Khơi nguồn tội ác](https://thanhdo89se.github.io/2018/chapter01-the-origin-of-crime/)

[Chapter 2: Raise of the North Force - Thế lực phương Bắc](https://thanhdo89se.github.io/2018/chapter02-raise-of-the-north-force/)

[Chapter 3: Chasing the Shark - Thám tử Cá Mập](https://thanhdo89se.github.io/2018/chapter03-chasing-the-shark/)

[Chapter 4: Reveal the Secret - Giải mã bí mật](https://thanhdo89se.github.io/2018/chapter04-reveal-the-secret/)

Chapter 5: The art of stealing - Nghệ thuật kiếm chác

Chapter 6: Raise of the South Force - Thế lực miền Nam

Chapter 7: Expansion of the core - Phiên bản mở rộng

Chapter 8: War of Gangs - Chiến tranh ảo

Chapter 9: The last battles and face of Boss - Đàn áp

Chapter 10: The end of crime - Kết thúc 

Chapter 11: Má ơi dài quá T.T

---

# This is not "extra-ordinary" things!

Phần code trong series này được viết bằng Haskell.

Nói thế thôi các bạn đừng sợ, Haskell rất đẹp, Haskell không khó như bạn nghĩ.

Tôi sẽ cố gắng giải thích code mà tôi viết, anw thì các bạn đọc series này cũng cần một chút hiểu biết về lập trình.

Có thể đọc xong series các bạn sẽ muốn làm quen với Haskell, tôi cũng muốn nhắn nhủ rằng, hãy học đi, ko khó đâu, ko cao siêu gì đâu ^_*

---

# This is ...?