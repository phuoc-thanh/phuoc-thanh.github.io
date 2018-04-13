---
layout: post
title: "Monoid, Functor - Định nghĩa và ứng dụng"
comments: true
description: "Monoid, Functor - Định nghĩa và ứng dụng"
keywords: "monoid, functor, binary operation, algebra, math, category, abstract, functional, programming, haskell"
---

Mày mò dịch thuật, tổng hợp, sắp xết để tóm tắt về một chủ đề khá trừu tượng. Viết để nhớ, viết để học, và để chia sẻ...

## 1. Định nghĩa Monoid

Monoid là 1 khái niệm xuất phát từ Đại Số Trừu Tượng (Abstract Algebra) , cụ thể hơn: Lý Thuyết Phạm Trù (Category Theory)
 
> A monoid is an algebraic structure with a single associative binary operation and an identity element

### 1.1 Binary Operation

**Định nghĩa**

Trong toán học, ***Binary Operation*** là phép toán trong 1 tập S, nó kết hợp 2 phần tử (còn gọi là toán hạng) của tập S để tạo ra 1 phần tử khác cũng thuộc tập S.

***Binary Operation*** có thể dịch là phép toán 2 ngôi hoặc phép toán nhị nguyên, là 1 phép toán sử dụng 2 biến đầu vào và cho ra 1 kết quả.

Ví dụ điển hình về phép toán nhị nguyên là phép cộng (+) và phép nhân (x) trên 1 tập đơn:
* Trong tập hợp số thực R, f(a, b) = a + b là 1 phép toán nhị nguyên vì tổng của 2 số thực là 1 số thực.

***Note:***

*Khác với Unary Operation là phép toán 1 ngôi (đơn nguyên), sử dụng 1 biến đầu vào và cho ra 1 kết quả.*

*Khác với Bitwise Operation thường được dịch là phép toán nhị phân, sử dụng cả Unary/Binary Operation để tính toán số nhị phân*


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

---

## 2. Monoid trong lập trình hàm (Haskell)

Xét 1 kiểu (type) m và 1 phép toán (<>) :: m -> m -> m. Kiểu m và phép toán (<>) được coi là monoid khi:
1. luôn tồn tại 1 phần tử mempty :: m thỏa điều kiện x <> mempty == x and mempty <> x == x;

2. và phép toán (<>) có tính kết (associative): (a <> b) <> c == a <> (b <> c).

### 2.1 Lớp Monoid (Monoid typeclass) trong Haskell

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

Và haskell có sẵn rất nhiều thực thể Monoid (Monoid instances). Ví dụ dễ thấy nhất là list:

```haskell
instance Monoid [a] where
  mempty  = []
  mappend = (++)
```

### 2.2 Ứng dụng Monoid (to be completed)

Monoid rất thông dụng trong haskell,

** The `Writer` Monad **

** The `Foldable` Class **

** Finger Trees **

** Options and settings **

---

## 3. Định nghĩa Functor

Functor cũng xuất phát từ Đại Số Trừu Tượng (Abstract Algebra) và Lý Thuyết Phạm Trù (Category Theory).

>A functor is a type of mapping between categories arising in category theory. Functors can be thought of as homomorphisms between categories. In the category of small categories, functors can be thought of more generally as morphisms.

### 3.1 Category

Category trong từ điển toán tin/kỹ thuật được dịch là "Phạm Trù", có lẽ là 1 từ vay mượn từ Triết Học. Vậy Category Theory được dịch là Lý Thuyết Phạm Trù, nghe thật "trừu tượng" và "hàn lâm" hehe. Từ đây, tôi viết Category cho ngắn gọn chứ Phạm Trù nghe cao siêu quá =)).

> Category theory is a formalism that allows a unified way for expressing properties and constructions that are similar for various structures.

Trong Toán học, Category là 1 cấu trúc đại số (Algebraic Structure). Category bao gồm 1 nhóm đối tượng (objects) được liên kết với nhau bởi những arrows.

Arrow: là khái niệm chỉ phép ánh xạ (morphism) giữa 2 đối tượng (objects). 

Ví dụ dễ thấy nhất của Category chính là sets, trong đó object chính là set và arrow là function.


**Tính chất**

Tính chất cơ bản của Category là kết hợp (composition of the arrows) (1).

Và sự tồn tại của 1 mũi tên định danh (identity arrow) cho mỗi object (2).

* Identity Arrow: là phép ánh xạ lên chính bản thân 1 object (self-morphism), nó sẽ không làm thay đổi object đó.

* Identity Arrow có vai trò giống như số 0 trong phép cộng và số 1 trong phép nhân, như identity element trong monoid vậy

(1) và (2) nghe quen quen nhỉ, he he?

Yep, Monoid và Category đều là cấu trúc nhóm ("Group-like" Structure). Monoid chính là 1 dạng Category đặc biệt gồm 1 object duy nhất với những ánh xạ đơn (morphisms) phản chiếu chính nó.
Category chính là 1 dạng khái quát hóa của Monoid.


### 3.2 Functor

Okay, tiếp nhé, đoạn này dịch từ wikipedia và wikiversity, hơi hại não.  

Functor cũng là khái niệm xuất phát từ Category Theory. Cụ thể, nó là 1 kiểu ánh xạ (mapping) giữa các Category.

Ví dụ ta có 2 Category là C và D, F được gọi là functor (covariant functor) từ C đến D khi:

* F ánh xạ mỗi object x thuộc C đến object F(x) thuộc D

* F ánh xạ mỗi arrow f:x -> y thuộc C đến arrow F(f):F(x) -> F(y) thuộc D

* F ánh xạ mỗi identity arrow: F(idx) = idF(x)

* F giữ tính kết hợp cho tất cả ánh xạ: F(g ⚬ f) = F(g) ⚬ F(f)  

Còn 1 thể loại contravariant functor thì đảo ngược chiều của arrow.

---

## 4. Functor trong lập trình hàm (Haskell)

Sau khi đã đọc hết mớ lý thuyết về functor, giờ ta sẽ xem cách nó được hiện thực hóa vào lập trình (Haskell).

Trước tiên, các bạn hãy hiểu phép ánh xạ (Morphism) trong toán học chính là function trong Haskell đã nhé.

### 4.1 Lớp Functor (Functor typeclass)

Haskell có 1 lớp tên là Functor và lớp này chỉ có 1 function duy nhất là fmap:

```haskell
class Functor f where
  fmap :: (a -> b) -> f a -> f b
```

fmap chính là 1 hàm đa kiểu (polytypic function) dùng để map function của những type đã tồn tại với function của những type mới.

### 4.2 Một vài ví dụ của các Functor instance (thực thể)

**List Functor**

```haskell
instance Functor [] where
  fmap = map
```
Nhìn vào định nghĩa thực thể functor trên list, ta có thể thấy fmap chính là dạng khái quát hóa của map.

```haskell
fmap (* 10)  [2,4,8,16] = [20,40,80,160]
--  Int->Int    [Int]         [Int]
```

**Maybe Functor**

```haskell
instance Functor Maybe where
  fmap _ Nothing  = Nothing
  fmap f (Just x) = Just (f x)
```
fmap chỉ áp dụng function trên kiểu Just x và bỏ qua kiểu Nothing

```haskell
fmap  (+7)    (Just 10)  = Just 17
fmap  (+7)     Nothing   = Nothing
--Int->Int     Maybe Int   Maybe Int  
```

**Custom data type Functor**

2 ví dụ trên là những thực thể Functor có sẵn trong gói Prelude của Haskell, chúng ta có thể tạo ra functor cho các kiểu dữ liệu tùy biến khác.

Ví dụ ta có 1 data type:

```haskell
data Tree a = Leaf a | Branch (Tree a) (Tree a) deriving (Show)
```

Ta có thể định nghĩa thực thể Functor cho kiểu Tree như sau:

```haskell
instance Functor Tree where
  fmap f (Leaf x)            = Leaf   (f x)
  fmap f (Branch left right) = Branch (fmap f left) (fmap f right)
```

Compile nó và thử apply function (2*) lên Tree này để xem điều kì diệu :D

```haskell
fmap (2*) (Branch (Branch (Leaf 1) (Leaf 2)) (Leaf 3))
```

### 4.3 Data.Functor

Các bạn xem link sau để tìm hiểu chi tiết về gói Data.Functor trong Haskell và các ví dụ khác

https://hackage.haskell.org/package/base-4.9.1.0/docs/Data-Functor.html

### 4.4 Functor Laws

Từ những ví dụ trên, ta có thể nhận thấy:

1. Functor nhận đối số (arguments) là 1 type constructor chứ ko đơn thuần là 1 type.

Type constructor trong những ví dụ trên là [], Maybe, Tree chứ không dích danh type [Int] hay Maybe Bool... nào cả.  

2. Functor chỉ tính toán trên dữ liệu và không thay đổi cấu trúc của dữ liệu

### 4.4 Ích lợi gì khi dùng Functor? (to be completed)

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
http://stackoverflow.com/questions/13134825/how-do-functors-work-in-haskell
