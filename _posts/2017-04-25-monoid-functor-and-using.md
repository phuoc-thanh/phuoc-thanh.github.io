---
layout: post
title: "Monoid, Functor - Định nghĩa và ứng dụng trong lập trình"
comments: true
description: "Monoid, Functor - Định nghĩa và ứng dụng trong lập trình"
keywords: "monoid, functor, binary operation, algebra, math, category, abstract, functional, programming"
---

## Vài dòng

Mục đích của bài này là gì?

Là tại đang học Haskell, mà đụng tới mấy khái niệm mới mẻ quá. Tìm hiểu thêm tí thì biết là tại mình ko có nền tảng Đại Số vững chắc. Hồi ĐH hình như chỉ đc học giải tích thôi thì phải =)).  

Nên là, mày mò dịch thuật, tổng hợp, suy xét để viết ra bài này. Viết để nhớ, ko mai mốt lại quên. Viết cũng là 1 cách hữu ích trong tìm tòi/nghiên cứu để hiểu sâu hơn.

## 1. Định nghĩa Monoid

Monoid là 1 khái niệm xuất phát từ Đại Số Trừu Tượng (Abstract Algebra) , cụ thể hơn là trong lĩnh vực Lý Thuyết Phạm Trù (Category Theory)
 
> A monoid is an algebraic structure with a single associative binary operation and an identity element

### 1.1 Binary Operation - phép toán nhị nguyên

**Định nghĩa**

Trong toán học, Binary Operation là phép toán trong 1 tập S, nó kết hợp 2 phần tử (gọi là toán hạng) của tập S để tạo ra 1 phần tử khác thuộc tập S.

Binary Operation có thể dịch là phép toán 2 ngôi hoặc phép toán nhị nguyên, là 1 phép toán sử dụng 2 biến đầu vào và cho ra 1 kết quả.
* Khác với Unary Operation là phép toán 1 ngôi, phép toán đơn nguyên, sử dụng 1 biến đầu vào và cho ra 1 kết quả.
* Khác với Bitwise Operation thường được dịch là phép toán nhị phân, sử dụng cả Unary/Binary Operation để tính toán số nhị phân.  

Ví dụ điển hình về phép toán nhị nguyên là phép cộng (+) và phép nhân (x) trên 1 tập đơn:
* Trong tập hợp số thực R, f(a, b) = a + b là 1 phép toán nhị nguyên vì tổng của 2 số thực là 1 số thực.

**Tính chất**

Một phép toán nhị nguyên có thể có tính giao hoán, hoặc kết hợp. Ví dụ:

Đối với a,b,c là phần tử thuộc tập số thực R:

Phép cộng (+) có cả tính kếp hợp: (a + b) + c = a + (b + c) và giao hoán: a + b = b + a 

Phép trừ (-) ko có tính kếp hợp a − (b − c) ≠ (a − b) − c và cũng ko có tính giao hoán: a − b ≠ b − a

### 1.2 Monoid

Theo đó, Monoid là 1 cấu trúc đại số (Algebraic Structure) bao gồm 1 phép kết nhị nguyên (Associative Binary Operation) và 1 phần tử nhận dạng (Identity Element). Phép kết nhị nguyên ở đây có thể hiểu là phép toán nhị nguyên có tính kết hợp như phép cộng (+) và phép nhân (×).

**Định nghĩa**

Giả sử S là 1 tập hợp (set), và • là 1 phép toán nhị nguyên S × S → S, thì S cùng với • là 1 monoid nếu thỏa 2 điều sau:

1.Tính kết hợp: Đối với toàn bộ a,b và c thuộc S, ta luôn có (a • b) • c = a • (b • c)

2.Phần tử nhận dạng: Tồn tại 1 phần tử e thuộc S sao cho với từng phần tử a thuộc S, ta luôn có  e • a = a • e = a

**Ví Dụ**

Tập hợp số tự nhiên N, tạo ra 2 commutative monoid (monoid có tính giao hoán) với phép cộng (phần tử nhận dạng: 0) và phép nhân (phần tử nhận dạng 1)

## 2. Monoid trong lập trình hàm (Haskell)

Xét 1 kiểu (type) m và 1 phép toán (<>) :: m -> m -> m. Kiểu m và phép toán (<>) được coi là monoid khi:
1. luôn tồn tại 1 phần tử mempty :: m thỏa điều kiện x <> mempty == x and mempty <> x == x;

2. và phép toán (<>) có tính kết (associative): (a <> b) <> c == a <> (b <> c).

### 2.1 Lớp Monoid (Monoid typeclass)

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

Và haskell có sẵn rất nhiều thực thể Monoid (Monoid instances). Ví dụ dễ thấy nhất trong list:

```haskell
instance Monoid [a] where
  mempty  = []
  mappend = (++)
```

### 2.2 Ứng dụng Monoid

Monoid rất thông dụng trong haskell,

** The `Writer` Monad **

** The `Foldable` Class **

** Finger Trees **

** Options and settings ""

## 3. Định nghĩa Functor

Functor cũng xuất phát từ Đại Số Trừu Tượng (Abstract Algebra) và Lý Thuyết Phạm Trù (Category Theory).

>A functor is a type of mapping between categories arising in category theory. Functors can be thought of as homomorphisms between categories. In the category of small categories, functors can be thought of more generally as morphisms.

### 3.1 Category

Category trong từ điển toán tin/kỹ thuật được dịch là "Phạm Trù", đây có lẽ là 1 từ vay mượn từ môn Triết Học. Vậy Category Theory được dịch là Lý Thuyết Phạm Trù, nghe thật "trừu tượng" và "hàn lâm" hehe. Thôi thì từ đây tôi viết Category cho ngắn gọn chứ Phạm Trù nghe cao siêu quá =)).

> Category theory is a formalism that allows a unified way for expressing properties and constructions that are similar for various structures.

Trong Toán học, Category là 1 cấu trúc đại số (Algebraic Structure) - cũng như Monoid. Cấu trúc Category bao gồm 1 nhóm đối tượng (objects) được liên kết với nhau bởi những arrows.

Arrow: là khái niệm chỉ phép ánh xạ (morphism) giữa 2 đối tượng (object). 

Ví dụ dễ thấy nhất của Category chính là sets, object chính là set và arrow là function.


**Tính chất**

Tính chất cơ bản của Category là kết hợp (composition of the arrows) (1).

Và sự tồn tại của 1 mũi tên định danh (identity arrow) cho mỗi object (2).

* Identity Arrow: là phép ánh xạ lên chính bản thân 1 object (self-morphism), nó sẽ không làm thay đổi object đó.

* Identity Arrow có vai trò giống như số 0 trong phép cộng và số 1 trong phép nhân, như identity element trong monoid vậy

(1) và (2) nghe quen quen nhỉ, he he?

Yep, Monoid và Category đều là cấu trúc nhóm ("Group-like" Structure). Monoid chính là 1 dạng Category đặc biệt gồm 1 object duy nhất với những ánh xạ đơn (morphisms) phản chiếu chính nó.
Category chính là 1 dạng khái quát hóa của Monoid.

Nếu có tgian thì tôi sẽ đọc thêm về Arrow, Object và Category Theory để hiểu thêm đoạn này.

### 3.2 Functor

Okay, tiếp nhé, đoạn này tôi dịch từ wikipedia và wikiversity, hơi hại não.  

Functor cũng là khái niệm xuất phát từ Category Theory. Cụ thể, nó là 1 kiểu ánh xạ (mapping) giữa các Category.

Ví dụ ta có 2 Category là C và D, F được gọi là functor (covariant functor) từ C đến D khi:

* F ánh xạ mỗi x object thuộc C đến object F(x) thuộc D

* F ánh xạ mỗi arrow f:x -> y thuộc C đến arrow F(f):F(x) -> F(y) thuộc D

* F ánh xạ mỗi identity arrow: F(idx) = idF(x)

* F giữ tính kết hợp cho tất cả ánh xạ: F(g ⚬ f) = F(g) ⚬ F(f)  

Còn 1 thể loại contravariant functor thì đảo ngược chiều của arrow.

## 4. Functor trong lập trình hàm (Haskell)

Sau khi đã đọc hết mớ lý thuyết về functor, giờ ta sẽ hiện thực hóa nó vào lập trình (Haskell).

Trước tiên, các bạn hãy hiểu phép ánh xạ (Morphism) trong toán học chính là function trong Haskell đã nhé.

### 4.1 Lớp Monoid (Monoid typeclass)

Haskell có 1 lớp tên là Functor và lớp này chỉ có 1 function duy nhất là fmap:

```haskell
class Functor f where
  fmap :: (a -> b) -> f a -> f b
```

fmap chính là 1 hàm đa kiểu (polytypic function) dùng để map hàm của những type đã tồn tại với hàm của những type mới.


## Tham khảo
https://en.wikiversity.org/wiki/Introduction_to_Category_Theory/Monoids
https://en.wikiversity.org/wiki/Introduction_to_Category_Theory/Functors
https://en.wikipedia.org/wiki/Binary_operation
https://en.wikipedia.org/wiki/Abstract_algebra
https://en.wikipedia.org/wiki/Category_(mathematics)
https://en.wikipedia.org/wiki/Morphism
https://en.wikipedia.org/wiki/Functor
http://www.cis.upenn.edu/~cis194/spring15/lectures/04-typeclasses.html
https://en.wikibooks.org/wiki/Haskell/Monoids
https://en.wikibooks.org/wiki/Haskell/The_Functor_class
https://en.wikibooks.org/wiki/Haskell/Foldable