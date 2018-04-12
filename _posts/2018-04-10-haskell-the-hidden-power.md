---
layout: post
title: "Haskell - Sức mạnh tiềm ẩn"
comments: true
description: "Haskell - Sức mạnh tiềm ẩn"
keywords: "haskell, pure, functional, hidden power, charm, beauty"
---

# Chapter 1. Câu chuyện về lập trình hàm (Functional Programming)

![Lambda Calculus](/assets/images/lambda_calculus.png)

Note: Để tiện cho việc đọc - hiểu, tôi xin giữ nguyên bản ko dịch một số từ ngữ như: Functional Programming, Declarative, Imperative, Compiler...

---

## 1.1 Imperative và Declarative Programming

Để tìm hiểu về Functional Programming, trước hết chúng ta nghía qua khái niệm Declarative Programming và Imperative Programming.

***Imperative Programming:*** Khi lập trình viên (ltv) sẽ viết code để chỉ cho compiler làm những gì họ muốn, chi tiết từng bước một: làm bước a, sau đó làm bước b, lặp lại bước a,b...

***Declarative Programming:*** Ltv sẽ viết code để mô tả những gì họ muốn nhưng không chỉ rõ chi tiết cách để lấy được kết quả


Ví dụ, khi tôi muốn có tập hợp số bi chẵn của 1 bàn billard.

Với kiểu lập trình Imperative, như C#/Java tôi sẽ code như sau:

```java
List<int> billard_balls = new List<int> {1, 2, 3, 4, 5, 6, 7, 8, 9};

List<int> results = new List<int>();
foreach(var ball in billard_balls)
{
    if (ball % 2 != 0)
          results.Add(ball);
}
```

Còn với kiểu lập trình Declarative, như sql sẽ là:

```sql
select ball from billard_balls where ball % 2 = 0
```

Các ngôn ngữ đại diện cho Imperative Programming: C++, Java, Python, Ruby, Swift...

Các ngôn ngữ đại diện cho Declarative Programming: Analytica, SQL, Haskell, Idris...

Ở danh sách Declarative, tôi có liệt kê Haskell và Idris, đây là 2 ngôn ngữ thiết kế theo mô hình lập trình hàm thuần túy: Pure Functional Programming.
Pure Functional chính là một nhánh (sub-set) của Declarative Programming.

Những ngôn ngữ có hỗ trợ lập trình hàm như C++, Java, Python và những ngôn ngữ lập trình hàm ko thuần túy như F#, Clojure, JavaScript.. thì không được xếp vào mục Declarative Programming

---

## 1.2 Lịch sử Functional Programming

Functional Programming có nguồn gốc từ Lambda Calculus (phép tính Lambda?) - còn Lambda Calculus là gì, chắc để viết sau vậy :) Nói chung là tập trừu tượng trong Toán Học Logic, được giới thiệu lần đầu khoảng thập niên 30.

Lisp - có thể coi là ngôn ngữ đầu tiên mang triết lý Functional Programming, được phát triển ở MIT cuối thập niên 50. Thật ra những phiên bản đầu tiên của Lisp là multi-paradigm language, tức là một ngôn ngữ đa dụng (đa triết lý). Những nn kế thừa của Lisp và các nhánh nhỏ từ Lisp thì được tập trung phát triển dựa trên nhân "functional" của Lisp hơn, như: Clojure, Julia.

Thập niên 70, Meta Language (ML), và sau đó là Miranda được tạo ra, đi kèm với giới thiệu chính thức về Functional Programming vào năm 77. ML có rất nhiều kế thừa, trong đó được nhiều ltv biết đến nhất là OCaml và Standard ML.

Haskell xuất hiện năm 87.

---

## 1.3 Functional - Các khái niệm cơ bản

Về các khái niệm, định nghĩa và đặc tính cơ bản của Functional Programming, có lẽ nên để các bạn tự tìm hiểu thêm. Tổng quan thì có 1 số điểm thiết yếu của Functional Programming như sau:

* **Higher Order Functions:** Hàm bậc cao như Fold, Map, Traversal, Composition.. Khám phá hết đống này, tôi đảm bảo các bạn sẽ lạc vào một chân trời trừu tượng mới.

* **Pure vs Impure:*** Tính thuần túy - Đây là vấn đề mơ hồ và còn nhiều tranh cãi, nhưng theo hiểu biết cá nhân thì Lambda Calculus mới có thể gọi là purest. Haskell có thể coi là chiến binh sống sót còn lại với chữ "Pure".

* **Recursion:** Đệ quy chính là vẻ đẹp của lập trình hàm. Có người từng nói, họ học Haskell chỉ vì "tail-recursive"

* **Lazy Evaluation:** Functional Programming mang đến những đặc điểm "nhàn rỗi" trong việc tính toán, rất nhiều thư viện có sẵn hỗ trợ việc tính toán nhàn rỗi. Nhưng hãy cẩn thận với Lazy IO, nhiều khi mang đến rắc rối hơn là tiện dụng

* **Type system:** Strongly Type n Weak-Type


# Chapter 2. Gọi tên Haskell

![Pure Functional Language](/assets/images/pure_functional.png)

Haskell, như tôi quảng cáo ở trên, được coi là chiến binh sống sót trong những vụ tranh cãi pure vs impure. Haskell ra mắt vào cuối thập niên 80, không phải là Pure Functional Language duy nhất, nhưng vị thế của Haskell đang dần được khẳng định. Haskell được thể hiện rõ ở các khía cạnh sau:


* **The Functional Aspect:** Thật ra khó mà giải nghĩa được chữ "functional" sao cho đúng và chính xác. Nhưng khi ta nói Haskell là functional, thì nó sẽ gợi lên 2 điểm:

    1. First-class của Haskell là Functions. Vậy một function f có thể tính toán dựa trên đối số (arguments) là 1 function g khác: f(g(x)).

    2. Haskell được thiết kế để `Đánh giá biểu thức` (Evaluation Expressions) thay vì `Thực thi câu lệnh` (Executing Instructions). Các bạn còn nhớ Declarative Programming vs Imperative Programming chứ? Yes, that's it.

* **The Pure Aspect:** Vẫn giữ những nét đặc trưng của Pure Functional, nhưng Haskell cho phép thực thi Impure code trong tầm kiểm soát. Điểm này chính là trọng tâm làm cho Haskell nổi bật nhất khi nói đến Pure Functional.

    Tính chất của Pure bao gồm: No mutation, No side-effects, Same input always make same output.

    Như vậy, Pure cũng đồng nghĩa với nói không với thao tác nhập xuất (IO), thậm chí Pure code còn ko thể in ra 1 thứ gì đó (print). Nghe nó quá thiếu thực tế, huh? Okay, Haskell gói những thứ impure lại và quản lý tách biệt nó một cách cực tốt. IO monads là bằng chứng mạnh mẽ nhất để Haskell chứng minh tính ứng dụng của nó trong thực tế.

* **The Lazy Aspect:** Haskell được thiết kế là 1 ngôn ngữ "nhàn rỗi, chậm tiêu" (a.k.a lazy), tức là khi cần đến thì mới làm, không chủ động tính toán trước. Với đặc điểm lazy này, Haskell mang đến lợi ích khi làm việc với cấu trúc dữ liệu, đặc biệt là cấu trúc vô hạn và tạo điều kiện để ltv viết code theo phong cách kết hợp (compositional programming style)


* **Statically Typed:** Haskell là ngôn ngữ có kiểu dữ liệu tĩnh, mọi biểu thức hay dữ liệu trong Haskell đều được kiểm tra kiểu (type-check) tại thời điểm compile. Mang đến lợi ích rất lớn khi loại trừ được nhiều lỗi hơn trước thời điểm run-time.


# Chapter 3. Haskell: Từ nghiên cứu đến ứng dụng



# Chapter 4. Thực tại và tiềm năng



# Reference

https://stackoverflow.com/questions/1784664/what-is-the-difference-between-declarative-and-imperative-programming
https://en.wikipedia.org/wiki/List_of_programming_languages_by_type
https://en.wikipedia.org/wiki/Functional_programming
https://en.wikipedia.org/wiki/Lambda_calculus
https://github.com/Gabriel439/post-rfc/blob/master/sotu.md