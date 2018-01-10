---
layout: post
title: "Hash Table là gì?"
comments: true
description: "The way hash table works"
keywords: "hashtable, hash, table, hash table, data structure"
---

## Trích dẫn

Đây là 1 bài dịch từ stackoverflow (có diễn giải thêm), tác giả trả lời câu hỏi: "Hash Table hoạt động như thế nào?"
> link: https://stackoverflow.com/questions/730620/how-does-a-hash-table-work

Phần tại hạ rất thích những câu trả lời kiểu Layman's Term như thế này, phần vì liên quan tới 1 số nghiên cứu nhỏ của tại hạ, nên cũng dịch và để đây, tạm lưu 1 bản tiếng Việt cho cấu trúc này.

## Giải thích Hash Table

Giả sử, bạn đang có 1 thư viện với vài nghìn ngăn tủ, và trong tay bạn có vài chục nghìn cuốn sách cần được lấp đầy vào các tủ đó. Nhưng ko chỉ vậy, bạn muốn có 1 cách sắp xếp nào đó để bạn có thể dễ dàng tìm đúng cuốn sách mà bạn đã bỏ vào ngăn lúc cần thiết.

Và bạn, chủ nhà sách (thư viện) quyết định, để dễ sử dụng, khi ai đó cần tìm sách, họ chỉ cần nhớ tên chính xác tựa sách (book title), việc còn lại, thủ thư sẽ chỉ cho bạn vị trí cuốn sách nhanh nhất, và dễ dàng nhất.

Vậy thì, làm cách nào? Thông thường bạn sẽ sắp xếp sách theo thứ tự, chủng loại và ghi chép lại vào 1 danh sách kèm 1 bản đồ nhỏ. Việc này sẽ tiết kiệm thời gian và công sức so với việc kiểm tra các ngăn/kệ/tủ sách trực tiếp. Nhưng bạn lại muốn hơn thế nữa, một cách nào đó sẽ chỉ chính xác địa chỉ ngăn tủ của cuốn sách cần tìm.

Okay, để thực hiện được việc sắp xếp sách như bạn muốn trên kia, sẽ cần kha khá công sức khi bạn xếp sách vào ngăn tủ. Thay vì bạn cứ xếp bừa, thì bạn dùng 1 chương trình tính toán nào đó, nhập vào tựa sách (book title) và chương trình đó sẽ in ra 1 vị trí ngăn tủ (unique address) cho cuốn sách đó. Và đó chính là nơi mà bạn sẽ xếp cuốn sách đó vào. Tất nhiên địa chỉ này phải là duy nhất tương ứng với tựa sách, để khi có ai khác tìm sách, bạn chỉ việc nhập lại tên tựa sách vào chương trình và sẽ lấy được địa chỉ chính xác vị trí cuốn sách.

Chương trình tính toán trên thường được gọi là Hash Algorithm (or Hash Function), nói đơn giản Hash Function sẽ là phép tính toán để cho ra con số cụ thể (duy nhất?) ứng với mỗi một dữ liệu nhập vào.

Kết hợp của kiến trúc gồm:

1. Dữ liệu cần tìm, ở ví dụ này là Địa chỉ ngăn chứa sách (The Value)
2. Chìa khóa tìm kiếm, ở đây là tựa sách (The Key)
3. Chương trình tính toán (The Hash Function)

Thì được gọi là Hash Table

## Về Hash Function

Về hash function, có rất nhiều vấn đề xung quanh nó như Collision, Complexity... Rất phức tạp để thiết kế một hash function mạnh + chính xác.
Ở đây tại hạ chưa đủ kinh nghiệm để viết tiếp.

Dẫn link wiki về Perfection Hash Function để chư vị đọc thêm: https://en.wikipedia.org/wiki/Perfect_hash_function

Sẽ edit thêm nếu có nghiên cứu phần này.