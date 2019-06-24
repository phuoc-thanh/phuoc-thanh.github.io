---
layout: post
title: "Monoid, Functor - Định nghĩa và ứng dụng"
comments: true
description: "Monoid, Functor - Định nghĩa và ứng dụng"
keywords: "monoid, functor, binary operation, algebra, math, category, abstract, functional, programming, haskell"
---

Khi bắt đầu tiếp xúc với Functional Programming, Tôi gặp nhiều khái niệm mới mẻ - đáng ngạc nhiên hơn là 5 năm lập trình dạo Tôi chưa hề nghe qua. Monoid, Functor và Monad là ba trong số đó.

Cũng đã dành kha khá thời gian của mình cho chủ đề khá trừu tượng này, nên Tôi quyết định viết đôi dòng ngắn ngắn tóm tắt về monoid và functor.

---

## 1. Monoid.. là gì?

Khái niệm Monoid có xuất phát từ Đại Số Trừu Tượng (Abstract Algebra), cụ thể hơn là Category Theory. Riêng về Category Theory, theo tôi là môn lý thuyết rất đáng bỏ thời gian ra học, nếu bạn nghiêm túc muốn lập trình với mức độ trừu tượng cao.
 
> A monoid is an algebraic structure with a single associative binary operation and an identity element

Trên đây là định nghĩa tổng quát của Monoid, với chỉ một câu ngắn gọn, mà buộc người đọc phải tìm và đọc thêm kha khá bài viết "toán học" khác chỉ để hiểu được định nghĩa. Bây giờ bạn thấy bắt đầu phức tạp rồi đó. 

### 1.1 Binary Operation

Trong toán học, ***Binary Operation*** là phép toán trong 1 tập S, nó kết hợp 2 phần tử (còn gọi là toán hạng) của tập S để tạo ra 1 phần tử khác cũng phải thuộc tập S.***Binary Operation*** còn được biết đến với tên gọi phép toán nhị nguyên, sử dụng 2 biến đầu vào và cho ra 1 kết quả.

Phép cộng (+) và phép nhân (x), chính là phép toán nhị nguyên mà ai-cũng-từng-biết.
* Trong tập hợp số thực R, f(a, b) = a + b là 1 phép toán nhị nguyên vì tổng của 2 số thực là 1 số thực.

*Lưu ý rằng Binary Operation khác với Unary Operation - phép toán đơn nguyên, và cũng khác với Bitwise Operation thường được dịch là phép toán nhị phân*


**Tính chất của Binary Operation**

Một phép toán nhị nguyên có thể có tính giao hoán, hoặc kết hợp. Ví dụ:

Đối với a,b,c là phần tử thuộc tập số thực R:

* Phép cộng (+) có cả tính kếp hợp: (a + b) + c = a + (b + c) và giao hoán: a + b = b + a 

* Phép trừ (-) ko có tính kếp hợp a − (b − c) ≠ (a − b) − c và cũng ko có tính giao hoán: a − b ≠ b − a

### 1.2 Monoid

Theo đó, Monoid là 1 cấu trúc đại số (Algebraic Structure) bao gồm 1 phép kết nhị nguyên (Associative Binary Operation) và 1 phần tử nhận dạng (Identity Element). Phép kết nhị nguyên ở đây có thể hiểu là phép toán nhị nguyên có tính kết hợp như phép cộng (+) và phép nhân (×).

**Định nghĩa**

Giả sử S là 1 tập hợp (set), và • là 1 phép toán nhị nguyên S × S → S, thì S cùng với • là 1 monoid nếu thỏa 2 điều sau:

1.Tính kết hợp: Đối với toàn bộ a,b và c thuộc S, ta luôn có (a • b) • c = a • (b • c)

2.Phần tử nhận dạng: Tồn tại 1 phần tử e thuộc S sao cho với từng phần tử a thuộc S, ta luôn có  e • a = a • e = a

*Ví dụ, Tập số tự nhiên N tạo ra 2 commutative monoid (monoid có tính giao hoán) gồm phép cộng và phép nhân*

```haskell
(3 + 6) + 9 = 3 + (6 + 9)
 6 + 0  = 0 + 6 = 6
```

Và

```haskell
(4 * 6) * 8 = 4 * (6 * 8)
 4 * 1  = 1 * 4 = 4
```

---

## 2. Monoid trong lập trình hàm (Haskell)

Với thiết kế Mathematics-like của mình, Haskell xây dựng Monoid rất sát với định nghĩa toán học của nó. Tất cả Monoids trong Haskell đều tuân theo Monoid Laws, bắt buộc phải có phép tính kết hợp (<>) và phần tử nhận dạng mempty.

```haskell
(x <> y) <> z = x <> (y <> z) -- associativity
mempty <> x = x               -- left identity
x <> mempty = x               -- right identity
```


### 2.1 Lớp Monoid trong Haskell

Monoid Typeclass trong haskell được định nghĩa như sau:

```haskell
class Monoid m where
  mempty  :: m
  mappend :: m -> m -> m

  mconcat :: [m] -> m     -- this can be omitted from Monoid instances
  mconcat = foldr mappend mempty

(<>) :: Monoid m => m -> m -> m    -- infix operator for convenience
(<>) = mappend
```

Typeclass, cũng là một từ khoá mới đối với bạn đọc chưa có kinh nghiệm cùng Functional Programming, ở đây các bạn có thể xem nó giống như Interface trong Java/C# vậy. Thật ra có nhiều điểm khác biệt giữa Typeclass và Interface, nhưng điểm chung dễ nhận thấy ở đây chính là nội dung của chúng, đều là một bản thiết kế trừu tượng, thể hiện tính chất chung của nhiều kiểu dữ liệu khác nhau.

Và haskell có sẵn rất nhiều thực thể Monoid (Monoid instances). List là một ví dụ:

```haskell
instance Monoid [a] where
  mempty  = []
  mappend = (++)
```

### 2.2 Ứng dụng Monoid

Monoid rất thông dụng trong haskell, hầu như có mặt khắp mọi nơi và được dùng thường xuyên.

List là một Monoid, vậy Monoid giúp ích List như thế nào? Thử phép (<>) như định nghĩa trên List, là biết ngay thôi :)

```haskell
iAppend = [1] <> [2] <> [3, 4] -- output: [1,2,3,4]

sAppend = "I am " <> "The " <> "Void" -- output: "I am The Void"
```

Ồ có vẻ như, cứ gặp một instance của Monoid, là chúng ta có một hàm concat free nhỉ. Và ngược lại, cứ thấy function (<>) ta hiểu là mình đang làm việc với một cấu trúc mang 2 tính chất Associative và has-Identity. Trên phương diện lập trình mà nói, Monoid tăng tính nhận diện và tổng quát cho ngôn ngữ.

Vẫn cảm thấy chưa đã, mời xem qua [Data.Monoid](http://hackage.haskell.org/package/base-4.12.0.0/docs/Data-Monoid.html), thư viện này cung cấp hàng loạt Monoid instance hay ho khác như Sum & Product cho Num type, hay instance cho Comparison, Predicate... 


**The `Foldable` Class**

Fold - hay Reduce trong một số ngôn ngữ khác, thuộc nhóm hàm bậc cao **Higher Order Functions**, và Haskell có Foldable class tổng quát hoá các tính toán xung quanh Fold như fold left, fold right, fold map và cả special case như sum, product, length, elem...

Nếu bạn xem mã của Foldable class, sẽ thấy nó được xây dựng từ Monoid. Ngay cả trong những ví dụ đơn giản, tính toán thông thường, chúng ta cũng dễ dàng nhận ra Fold và Monoid có gì đó... giống nhau?

```haskell
easySum = foldr (+) 0 [2,4,6,8] --output 20
maxFold = foldr max 66 [11,22,33,44,55] -- output 66
```

Có nhiều ví dụ thú vị hơn về foldable, như duyệt cây trong [blog này](http://blog.sigfpe.com/2009/01/haskell-monoids-and-their-uses.html) chẳng hạn:

```haskell
data Tree a = Empty | Leaf a | Node (Tree a) a (Tree a)
instance Foldable Tree where
    foldMap f Empty = mempty
    foldMap f (Leaf x) = f x
    foldMap f (Node l k r) = foldMap f l `mappend` f k `mappend` foldMap f r
```

Nếu ta define một cây như trên, sau đó ta cần duyệt cây để tìm phần tử giá trị bằng 1, hoặc bất cứ phần từ lớn hơn 5:

```haskell
tree = Node (Leaf 1) 7 (Leaf 2)

f1   = foldMap (Any . (== 1)) tree
f2   = foldMap (All . (>  5)) tree
```

---

## 3. Functor.. là gì?

Functor cũng xuất phát từ Category Theory giống như Monoid vậy, và nó còn trừu tượng hơn :)

> A functor is a type of mapping between categories arising in category theory. Functors can be thought of as homomorphisms between categories. In the category of small categories, functors can be thought of more generally as morphisms.

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
data Tree a = Empty | Leaf a | Node a (Tree a) (Tree a) deriving Show
```

Ta có thể định nghĩa thực thể Functor cho kiểu Tree như sau:

```haskell
-- Instance of Functor, to use fmap()
instance Functor Tree where
  fmap f (Empty)             = Empty
  fmap f (Leaf l)            = Leaf (f l)
  fmap f (Node n left right) = Node (f n) (fmap f left) (fmap f right)
```

Compile nó và thử apply function (2*) lên tree để xem điều kì diệu :D

```haskell
tree = Node 1 (Node 2 (Node 4 (Leaf 7) Empty) (Leaf 5))
              (Node 3 (Node 6 (Leaf 8) (Leaf 9)) Empty)
fmap_test = fmap (2*) tree
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

https://en.wikipedia.org/wiki/Morphism

http://www.cis.upenn.edu/~cis194/spring15/lectures/04-typeclasses.html

https://en.wikibooks.org/wiki/Haskell/Monoids

https://en.wikibooks.org/wiki/Haskell/The_Functor_class

http://stackoverflow.com/questions/13134825/how-do-functors-work-in-haskell
