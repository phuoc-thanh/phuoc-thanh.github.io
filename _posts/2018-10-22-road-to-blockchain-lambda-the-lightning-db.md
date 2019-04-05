---
layout: post
title: "Lambda Chain: The Lightning Database"
comments: true
description: "Road to Blockchain: Database"
keywords: "blockchain, bitcoin, haskell, lambda, LMDB, Lightning, Memory-Mapped, database, memory"
---

Khi khởi động một dự án, ở giai đoạn thiết kế tổng thể cấu trúc hệ thống, khâu quyết định công cụ lưu trữ dữ liệu thường bị xem nhẹ và diễn ra cũng rất nhanh gọn. Chúng ta mặc định trong đầu những lựa chọn khá hạn chế xung quanh SQL / NoSQL, và ko nghĩ rằng sự lựa chọn đó đòi hỏi phức tạp hay khó khăn. MySQL, MsSQL, MongoDb, SQL Lite, Redis.. cứ thế mà pick, gần như chỉ dựa trên yếu tố "quen tay".

Liệu có một lúc nào đó, khi không có áp lực nào thúc ép, tính hiếu kỳ có gây cảm hứng cho một lập trình viên bình thường suy nghĩ về CSDL (Database) theo cách khác thường?

Computer là cỗ máy có nhiều loại bộ nhớ và nơi lưu trữ khác nhau, vậy những MySQL, Redis, Mongodb mà chúng ta vẫn hay sử dụng lưu dữ liệu ở đâu? Trên Disk, trên RAM, hay.. CPU Cache-Mem?

Một câu hỏi tuy đơn giản nhưng sâu sắc.

..

## Computer Memory & Storage

Để trả lời cho câu hỏi trên, tôi đã tìm lại chút kiến thức sơ đẳng về bộ nhớ máy tính.

Bộ nhớ - Memory/Storage trong một hệ thống tính toán chuẩn, thường được phân loại theo 2 loại hình chính:

* Main Memory - Bộ nhớ sơ cấp: Theo kiến trúc von Neumann thì Main Memory là nơi chứa các tập lệnh (instructions) và dữ liệu (data) dành cho sự truy cập tức thời của CPU. Các thế hệ CPU mới còn có thêm CPU Cache, cũng dùng chung mục đích nhưng bị hạn chế bởi dung lượng và sự bất kiểm soát.

Main Memory từng được chế tạo từ Cathode Ray Tube (vâng CRT, màn hình xê rờ tê đó các bạn), Magnetic Drum, Rings of Magnetic và hiện tại hầu hết là dùng DRAM.

* Secondary Storage - Bộ nhớ thứ cấp: Tất cả những nơi lưu trữ còn lại ngoài Main Memory thì được xếp vào đây. Băng từ, giấy đục lỗ, đĩa cứng và mới nhất là flash memory là vật liệu cấu thành Secondary Storage.

**Và câu trả lời là?**

RAM hay Disk đều có thể trở thành nơi lưu trữ dữ liệu, ltv có toàn quyền lựa chọn địa điểm lưu trữ, định dạng dữ liệu, và cả cách thức lưu trữ. Chọn Ram hay Disk, đều có những ưu điểm, nhược điểm riêng, tốc độ thường đi đôi với rủi ro và chi phí. DBMS được coi là lựa chọn cách thức lưu trữ, dù lưu ở đâu cũng sẽ có DBMS phù hợp hết, chúng ta ko cần phải quá lo lắng.

Nhưng có thể ko phải ai cũng biết, còn có một cách lưu trữ ít nổi tiếng hơn, tên gọi là memory-map, sử dụng cả RAM lẫn Disk để phục vụ cho công việc đọc/ghi dữ liệu.

## Single-level Store

Dựa trên một công nghệ cũ là Single-level store được giới thiệu cùng với sự xuất hiện của cỗ máy [Multics](http://gunkies.org/wiki/Multics) huyền thoại.

Bàn về lý thuyết của SLS trước nhé.

Ở trên tôi có đưa ra vấn đề là máy tính có rất nhiều nơi lưu trữ và ltv cần đưa ra quyết định chọn nơi nào để lưu.

## Memory-map files

**Virtual Memory**

Xét thêm về nhu cầu đọc/ghi dữ liệu thực hiện trên Computer, những phương thức cơ bản thường được sử dụng như open(), read(), write(), close()... được lõi hệ điều hành (OS Kernel) cung cấp khá đầy đủ. Tất nhiên system calls còn rất nhiều phương thức hay ho khác nữa, một trong số đó là mmap() - chính là nơi xuất phát của ý tưởng Memory-Mapped Database.

[System Calls - Linux](https://linux.die.net/man/2/)

**Vậy memory-map là gì? mmap() hoạt động như thế nào?**

Mmap() là hàm chức năng của hệ thống mà hầu hết OS, chuẩn POSIX hay Windows đều hỗ trợ. Mmap() khi được gọi sẽ tạo ra tham chiếu (mapping) giữa tập tin nguồn và bộ nhớ. Việc mapping này được thực thi tại bộ nhớ ảo của Process, not RAM or Disk itself.

Từ lúc mapping thành công trở đi, công đoạn quản lý quá trình chia vùng nhớ, bảng địa chỉ tham chiếu, tải nội dung lên RAM, lưu nội dung xuống file, giải phóng bộ nhớ trống... những công việc khó khăn, được OS Kernel gánh vác hết.

Có 2 kiểu mapping chính là file-backed và anonymous, khác biệt giữa chúng là dữ liệu sau khi đc mapping có lưu lại xuống file hay xoá sổ hoàn toàn.

Về virtual memory và file-mapping các bạn có thể tham khảo thêm nguồn khác vì mình ko chuyên về system nên chỉ có thể giải thích trong giới hạn hiểu biết.

Đây là một cuốn sách có viết về memory management khá chi tiết của linux và kiến trúc x86 của Gorman:
https://www.kernel.org/doc/gorman/

Ngoài ra tôi tìm được series youtube giải thích rất hay và rõ ràng về công nghệ virtual memory, tác giả kênh yt là [David Black-Scaffer](https://www.youtube.com/channel/UCzf_XjIoKSf4Ve2fH7xn-3A/feed)
https://www.youtube.com/playlist?list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX

## The Lightning

### Inherit from Single Value Store

### Born from Berkerley Database - BDB

Cải tiến từ Berkerley Database để khắc phục những khuyết điểm của người tiền nhiệm này.


# Reference

http://www.lmdb.tech/doc/
https://symas.com/lmdb/technical/

https://www.kernel.org/doc/gorman/pdf