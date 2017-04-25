---
layout: post
title: "Monoid - định nghĩa và ứng dụng trong lập trình"
comments: true
description: "Monoid - định nghĩa và ứng dụng trong lập trình"
keywords: "monoid, binary, functional, programming"
---

## 1. Định Nghĩa Monoid

Monoid là 1 khái niệm xuất phát trong Đại Số Trừu Tượng , cụ thể hơn là trong lĩnh vực Lý Thuyết Danh Mục (Category Theory)

> Category theory is a formalism that allows a unified way for expressing properties and constructions that are similar for various structures.

### Binary Operation - phép toán nhị nguyên

Trong toán học, Binary Operation là phép toán trong 1 tập S, nó kết hợp 2 phần tử (gọi là toán hạng) của tập S để tạo ra 1 phần tử khác thuộc tập S.

Binary Operation có thể dịch là phép toán 2 ngôi, phép toán nhị nguyên là 1 phép toán sử dụng 2 biến đầu vào và cho ra 1 kết quả.
* Khác với Unary Operation là phép toán 1 ngôi, phép toán đơn nguyên, sử dụng 1 biến đầu vào và cho ra 1 kết quả.
* Khác với Bitwise Operation thường được dịch là phép toán nhị phân, sử dụng cả Unary/Binary Operation để tính toán số nhị phân.  

Typical examples of binary operations are the addition (+) and multiplication (×) of numbers and matrices as well as composition of functions on a single set. For instance,

Ví dụ điển hình về phép toán nhị nguyên là phép cộng (+) và phép nhân (x) trên 1 tập đơn:
* Trong tập hợp số thực R, f(a, b) = a + b là 1 phép toán nhị nguyên vì tổng của 2 số thực là 1 số thực.

1 phép toán nhị nguyên có thể có tính giao hoán, hoặc kết hợp. Ví dụ:

Đối với a,b,c là phần tử thuộc tập số thực R:

Phép cộng (+) có cả tính kếp hợp: (a + b) + c = a + (b + c) và giao hoán: a + b = b + a 

Phép trừ (-) ko có tính kếp hợp a − (b − c) ≠ (a − b) − c và cũng ko có tính giao hoán: a − b ≠ b − a

### Monoid

Theo đó, Monoid là 1 cấu trúc đại số bao gồm 1 phép kết nhị nguyên (Associative Binary Operation) và 1 phần tử nhận dạng (Identity Element). Phép kết nhị nguyên ở đây có thể hiểu là phép toán nhị nguyên có tính kết hợp như phép cộng (+) và phép nhân (×).

**Định nghĩa**
Giả sử S là 1 tập hợp (set), và • là 1 phép phép toán nhị nguyên S × S → S, thì S cùng với • là 1 monoid nếu thỏa 2 điều sau:

1.Tính kết hợp: Đối với toàn bộ a,b và c thuộc S, ta luôn có (a • b) • c = a • (b • c)

2.Phần tử nhận dạng: Tồn tại 1 phần tử e thuộc S sao cho với từng phần tử a thuộc S, ta luôn có  e • a = a • e = a

**Ví Dụ**
Tập hợp số tự nhiên N, tạo ra 2 commutative monoid (monoid có tính giao hoán) với phép cộng (phần tử nhận dạng: 0) và phép nhân (phần tử giao hoán 1)

## Monoid trong lập trình hàm (Haskell)

Xét 1 kiểu (type) m và 1 phép toán (<>) :: m -> m -> m. Kiểu m và phép toán (<>) được coi là monoid khi:
1. luôn tồn tại 1 phần tử mempty :: m thỏa điều kiện x <> mempty == x and mempty <> x == x;

2. và phép toán (<>) có tính kết (associative): (a <> b) <> c == a <> (b <> c).

### Monoid typeclass

Lớp monoid trong haskell được định nghĩa như sau:

```haskell
class Monoid m where
  mempty  :: m
  mappend :: m -> m -> m

  mconcat :: [m] -> m     -- this can be omitted from Monoid instances
  mconcat = foldr mappend mempty

(<>) :: Monoid m => m -> m -> m    -- infix operator for convenience
(<>) = mappend
```
Và haskell có sẵn rất nhiều Monoid instances. Ví dụ dễ thấy nhất trong list:

```haskell
instance Monoid [a] where
  mempty  = []
  mappend = (++)
```

## Tham khảo

https://en.wikipedia.org/wiki/Monoid
https://en.wikipedia.org/wiki/Binary_operation
https://en.wikipedia.org/wiki/Abstract_algebra
http://www.cis.upenn.edu/~cis194/spring15/lectures/04-typeclasses.html