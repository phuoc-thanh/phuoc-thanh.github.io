---
layout: post
title: "Haskell - Sức mạnh tiềm ẩn"
comments: true
description: "Haskell - Sức mạnh tiềm ẩn"
keywords: "haskell, pure, functional, hidden power, charm, beauty"
---

# Chapter 1. Câu chuyện về lập trình hàm (Functional Programming)

Note: Để tiện cho việc đọc - hiểu, tôi xin giữ nguyên bản ko dịch một số từ ngữ như: Functional Programming, Declarative, Imperative, Compiler...

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

Còn những ngôn ngữ có hỗ trợ lập trình hàm như C++, Java, Python và những ngôn ngữ lập trình hàm ko thuần túy như F#, Clojure, JavaScript.. thì không được xếp vào mục Declarative Programming

## 1.2 Lịch sử Functional Programming

Functional Programming có nguồn gốc từ Lambda Calculus (phép tính Lambda?) - còn Lambda Calculus là gì, chắc để viết sau vậy :) Nói chung là tập trừu tượng trong Toán Học Logic, được giới thiệu lần đầu khoảng thập niên 30.

Lisp - có thể coi là ngôn ngữ đầu tiên mang triết lý Functional Programming, được phát triển ở MIT cuối thập niên 50. Thật ra những phiên bản đầu tiên của Lips là multi-paradigm language, tức là một ngôn ngữ đa dụng (đa triết lý). Những nn kế thừa của Lips và các nhánh nhỏ từ Lips thì được tập trung phát triển dựa trên nhân "functional" của Lips hơn, như: Clojure, Julia.

Thập niên 70, ML, và sau đó là Miranda được tạo ra, đi kèm với giới thiệu chính thức về lập trình hàm năm 77. ML có rất nhiều kế thừa, trong đó được nhiều ltv biết đến nhất là OCaml và Standard ML.

Haskell xuất hiện năm 87.

## 1.3 Các khái niệm cơ bản

Về các khái niệm, định nghĩa và đặc tính cơ bản của Functional Programming, có lẽ nên để các bạn tìm hiểu thêm. Tổng quan thì có 1 số điểm thiết yếu của Functional Programming như sau:

* Higher Order Functions: Hàm bậc cao như Fold, Map, Traversal, Composition.. Khám phá hết đống này, tôi đảm bảo các bạn sẽ lạc vào một chân trời trừu tượng mới.

* Pure vs Impure: Tính thuần túy - Đây là vấn đề mơ hồ và còn nhiều tranh cãi, nhưng theo hiểu biết cá nhân thì Lambda Calculus mới có thể gọi là purest. Haskell có thể coi là chiến binh còn sống sót còn lại với chữ "Pure".

* Recursion: Đệ quy chính là vẻ đẹp của lập trình hàm. Có người từng nói, họ học Haskell chỉ vì "tail-recursive"

* Type system: Strongly Type n Weak-Type

# Chapter 2. Gọi tên Haskell

Haskell, như tôi quảng cáo ở trên, được coi là chiến binh sống sót trong những vụ tranh cãi pure vs impure.

Haskell đủ "mature" để có thể tồn tại giữa hàng trăm ngôn ngữ khác nhưng vẫn giữ được mức độ Pure rất cao.

Haskell là ngôn ngữ tốt nhất dành cho những ai đang muốn học Functional Programming

Haskell thường được xem là ngôn ngữ học thuật, nghiên cứu. Nhưng gần đây đã xuất hiện những sản phẩm tạo ra từ Haskell


# Cái nhìn sâu hơn vào Haskell

## Language Syntax

## Compiler

## Build System (Stack - Cabal)

## Central lib repo: Hackage

# Từ nghiên cứu đến ứng dụng

# Thực tại và tiềm năng

## Haskell trong công nghiệp phần mềm

# Reference

https://stackoverflow.com/questions/1784664/what-is-the-difference-between-declarative-and-imperative-programming
https://en.wikipedia.org/wiki/List_of_programming_languages_by_type
https://en.wikipedia.org/wiki/Functional_programming
https://en.wikipedia.org/wiki/Lambda_calculus