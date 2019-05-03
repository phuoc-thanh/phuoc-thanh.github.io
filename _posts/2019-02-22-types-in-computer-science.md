---
layout: post
title: "Types trong Khoa Học Máy Tính - Draft"
comments: true
description: "Types in Computer Science"
keywords: "type, computer, science, programming, language"
---

Ai trong số chúng ta - những lập trình viên võ công thượng thừa cũng đã ít nhiều (lớn hơn zero) lần đọc đến và nghe qua những cuộc tranh cãi, so kè giữa các ngôn ngữ lập trình. Và có thể, cũng có đôi ba lần ta lớn gan tham gia vào cuộc lý luận, mà gay gắt hơn cả cuộc khẩu chiến 2 bên Chúa Nguyễn's fan club vs Nhà Tây Sơn's fellow, thâm sâu trừu tượng hơn cả "Republic" của Plato.

Cú pháp, hiệu suất, mức độ phủ sóng, hệ sinh thái, sản phẩm, tuổi đời, độ hot và cả lương lậu cũng được đem ra mổ xẻ, đặt lên bàn cân để so sánh. Trong cuộc cãi lộn, sau một gian đoạn khi mà quần hùng đã chán chê no nê với thống kê, tin tức, cả những đoạn code đanh thép thì sẽ chỉ còn lại những anh tài phân tích về Thiết Kế Ngôn Ngữ, đại loại như:

* Javascript có hướng đối tượng ko?

* Cơ chế quản lý Memory của Java cùi bắp?

* Nhóm ngôn ngữ Script-like luôn có tốc độ kém?

* Pointer của C++ là tội ác?

* ...

Một trong số những đặc điểm ảnh hưởng lớn tới thiết kế của ngôn ngữ, cũng thường được đem ra làm vũ khí chiến tranh là Type System: Statically Type vs Dynamically Type, Strong Type vs Weak Type.

Vậy Type là món công phu gì mà ngôn ngữ lập trình bắt buộc phải có? Tại hạ cũng đã bắt đầu tìm hiểu, và mở đầu bằng ghi chép này đây.

## 1. Type System là gì và đến từ đâu?

Trong một định nghĩa sách vở:

> A type system is a tractable syntactic method for proving the absence of certain program behaviors by classifying phrases according to the kinds of values they compute. (Pg 01, Type & Programming Language) [1]

Kèm theo với định nghĩa trên, lịch sử ghi nhận khái niệm về Type System xuất phát từ rất sớm - đầu thế kỷ 19 (1902) và bắt nguồn từ một số lĩnh vực nghiên cứu lớn hơn gồm: Logic học, Toán Học, Triết Học.

Tiền thân của nó là Type Theory, được phát minh với mục đích phòng tránh và loại trừ những sự kiện phi Logic (nghịch lý) trong Toán Học.

1. Type System sinh ra với mục đích tìm kiếm và chứng minh sự thiếu vắng một số hành vi trong một chương trình máy tính (computer program)

2. Type System làm việc đó như thế nào?

Nó phân loại nhừng từ, cụm từ trong mã nguồn của chương trình, dựa vào giá trị mà chúng (những từ, cụm từ đó) sẽ tính toán khi chương trình được thực thi.

Công việc của Type System: Classification of terms, còn có thể hiểu là một phép đo lường hành vi của một program. Phép đo này ước lượng độ "tĩnh" (Static) của các terms (thuật ngữ) của Program đó.

Cũng từ phép đo lường đó của Type System mà ngành Khoa Học Máy Tính, đặc biệt là trong phạm vi ngôn ngữ lập trình, sinh ra các khái niệm "Statically Type" và "Dynamically Type". Thực tế, định nghĩa đúng của 2 từ này phải là Statically checked, và Dynamically checked vì mức độ "tĩnh" của một ngôn ngữ được quyết định bởi TypeChecker.


## 2. Rốt cuộc, Type System mang lại ích lợi gì?

Nói như định nghĩa trên thì trừu tượng, giờ chúng ta cần tìm hiểu chi tiết hơn về những lợi ích mà Type System mang lại.

### Phát hiện lỗi

Lợi ích rõ ràng, và có lẽ là to lớn nhất mà Type System mang lại, là phát hiện lỗi từ rất sớm. Dễ dàng để nhận ra chi phí mà TypeChecker giúp chúng ta tiết kiệm khi phát hiện errors ở giai đoạn biên dịch, thay vì run-time, deploy phase. Về thời gian, tiền bạc, công sức, có lẽ ai cũng nhìn thấy rằng Type System & Type Checker là một cứu tinh - trời ban.

Nói xa hơn, khi thực nghiệm thì những ngôn ngữ Statically Type luôn giúp chương trình, ứng dụng có một độ tin cậy cao. Một khi Typechecker đã nói pass, có nghĩa là khả năng cao nó sẽ chạy trơn tru.

### Trừu tượng hoá (Abstraction)

Nghe rất thân quen nhưng đúng là Type System hỗ trợ tính trừu tượng trong lập trình.

Class và Interface chính là một phần của Type System

### Tài liệu hoá (Documentation)

Type Declaration/Notation chính là tài liệu rất đáng tin cậy và ko bao giờ bị lỗi thời, vì Compiler luôn luôn kiểm tra những chỉ mục này.

### Độ an toàn của ngôn ngữ


### Tính hiệu quả

Những Type System đầu tiên được kế, như trên Fortran, được giới thiệu rằng có thể giúp chương trình thực thi hiệu quả hơn. Một ví dụ dễ thấy khi TypeChecker có thể phân biệt các biểu thức trên số nguyên Integer và biểu thức trên số thực Real Numbers. Điều này cho phép Compiler có thể sử dụng các hình thức diễn đạt khác nhau và sinh ra mã máy thích hợp cho các Primitives Operations.

Các Compiler hiện đại vẫn phụ thuộc rất lớn vào Typechecker để tăng độ hiệu quả cho chương trình.


## 3. Ảnh hưởng của Type System đối với thiết kế Nn lập trình

Xin trích lời bình của một cao thủ:

> Well-typed programs don't go wrong, but not every program that never goes wrong is well-typed. It's easy to exhibit programs that don't go wrong but are ill-typed in ... any ... decidable type system. Many such programs are useful, which is why dynamically-typed languages like Erlang and Lisp are justly popular [2]

Ai cũng thấu hiểu, dynamic type được sử dụng rộng rãi và phổ biến, trong môi trường học thuật, startup hay doanh nghiệp... Simon ở đây muốn nói rằng sử dụng những ngôn ngữ này để tạo ra một chương trình chạy đúng thì dễ, và nó lại còn hữu ích. Vậy thì ai quan tâm tới 'statically typed'?

Đa phần, những dự án sử dụng statically type lang (Java, ) đều hướng đến mục đích ỔN ĐỊNH và ÍT RỦI RO. 