---
layout: post
title: "Lambda Chain: The Lightning Database"
comments: true
description: "Road to Blockchain: Database"
keywords: "blockchain, lambda, LMDB, Lightning, Memory-Mapped, database, memory"
---

Khi khởi động một dự án, ở giai đoạn thiết kế tổng thể cấu trúc hệ thống, khâu quyết định công cụ lưu trữ dữ liệu thường bị xem nhẹ và diễn ra cũng rất nhanh gọn. Chúng ta mặc định trong đầu những lựa chọn khá hạn chế xung quanh SQL / NoSQL, và ko nghĩ rằng sự lựa chọn đó đòi hỏi phức tạp hay khó khăn. MySQL, MsSQL, MongoDb, SQL Lite, Redis.. cứ thế mà pick, gần như chỉ dựa trên yếu tố "quen tay".

Liệu có một lúc nào đó, khi không có áp lực nào thúc ép, tính hiếu kỳ có gây cảm hứng cho một lập trình viên bình thường suy nghĩ về CSDL (Database) theo cách khác thường?

Computer là cỗ máy có nhiều loại bộ nhớ và nơi lưu trữ khác nhau, vậy những MySQL, Redis, Mongodb mà chúng ta vẫn hay sử dụng lưu dữ liệu ở đâu? Trên Disk, trên RAM, hay.. CPU Cache-Mem?

---

## 1. Computer Memory & Storage

Trước hết, chúng ta tìm hiểu về khái niệm bộ nhớ, lưu trữ của máy tính.

### Computer có những hình thức lưu trữ nào?

Đa phần những ghi chép và nghiên cứu trong ngành khoa học máy tính cho rằng Computer có 2 vùng lưu trữ chính là Main Memory và Secondary Storage, cũng có thể gọi tên phân biệt là "bộ nhớ" và "kho lưu trữ". Ngoài ra, những chíp vi xử lý mới còn có thêm bộ nhớ đệm (L1-L2-L3 Cache) cũng làm phần việc tương tự như Main Memory tuy nhiên dung lượng của Cache Mem rất nhỏ và ko nằm trong tầm quan sát/kiểm sát của người sử dụng.

* Main/Primary Memory: Theo kiến trúc von Neumann thì Main Memory là nơi chứa các tập lệnh (instructions) và dữ liệu (data) dành cho sự truy cập tức thời của CPU. RAM - như các bạn biết, là Memory của những chiếc PC hiện tại.

* Secondary Storage: Tất cả những nơi lưu trữ còn lại ngoài Main Memory thì được xếp vào Secondary Storage. Hard Disk Drive, Solid-state Drive là phần cứng lưu trữ phổ biến nhất hiện nay, được xem là Secondary Storage.

### Vậy dữ liệu nên được lưu ở đâu?

RAM hay Disk đều có thể trở thành nơi lưu trữ dữ liệu, ltv có toàn quyền lựa chọn địa điểm lưu trữ, định dạng dữ liệu, và cả cách thức lưu trữ. Chọn Ram hay Disk, đều có những ưu điểm, nhược điểm riêng, tốc độ thường đi đôi với rủi ro và chi phí.

Vì giá thành quá cao so với Disk Storage và tính chất volatile (Ko có điện, mất hết data) của RAM Memory, nên dữ liệu thường được ưu tiên lưu trên Disk, phần dữ liệu sử dụng thường xuyên hoặc những tác vụ đặc biệt thì lưu trên RAM.

Nhưng có thể ko phải ai cũng biết, còn có một cách lưu trữ ít nổi tiếng hơn, sử dụng cả RAM lẫn Disk để phục vụ cho công việc đọc/ghi dữ liệu. Công nghệ lưu trữ này có tên là memory-map, dựa trên mô hình Virtual Memory cùng triết lý Single-level Store.

---

## 2. Virtual Memory Concept

Những thế hệ computer đầu tiên, sự phân cấp bộ nhớ được thể hiện rất rõ ràng. Main/Primary Memory đắt đỏ, tốc độ cao nên chỉ dùng chứa mã thực thi - instructions và data thiết yếu nhất. Secondary Storage rẻ hơn, tất nhiên chậm chạp hơn làm những tác vụ còn lại.

Để tăng hiệu suất sử dụng của bộ nhớ và tận dụng tốt hơn nguồn tài nguyên của computer, các nhà khoa học máy tính đã rất nỗ lực tìm cách xoá đi ranh giới phân biệt giữa 2 cấp bộ nhớ này, và công nghệ được tạo ra sau cùng là Virtual Memory - phát minh quan trọng bậc nhất trong ngành KHMT.

### Nguồn gốc của bộ nhớ ảo

Những năm 40-50, với sự tồn tại của 2 cấp bộ nhớ kèm theo hạn chế của Memory, lập trình viên phải đảm nhiệm một công việc quan trọng là lên kế hoạch và tính toán các bước luân chuyển của dữ liệu giữa 2 cấp bộ nhớ. Công việc này chủ yếu là chia bộ nhớ ra thành từng blocks (về sau gọi là segments và pages), và tính toán thay đổi nơi lưu trữ của những block này (swap / overlay works).

Năm 1956, nhà Vật Lý học người Đức **Fritz-Rudolf Güntsch**, trong luận án tiến sĩ của mình, đã mô tả chiếc máy tính có khả năng tự điều chỉnh vùng nhớ - một cách tự động hoàn toàn.

Dựa trên bộ nhớ nhanh nhất thời điểm đó - lõi nhớ của siêu máy tính Whirlwind, ông lên ý tưởng chia bộ nhớ sơ cấp thành 6 blocks, mỗi block có dung lượng 100-words. Bộ nhớ này được sử dụng cùng với vùng tham chiếu địa chỉ (Address Space). Address Space có không gian tối đa là 1000 blocks, mỗi block cũng mang dung lượng 100-words.

> Whirlwind has a memory of 2K words, 16bits/word (4KB Memory)

Hình mô tả mô hình máy tính Güntsch:

![Güntsch’s virtual memory concept](/assets/images/1956_vm_concept.png)

* 6 blocks của Memory lần lượt chứa instructions ở 2 blocks M1, data ở 2 blocks M2, và vùng nhớ cố định ở 2 blocks M3 - là nơi được sử dụng để access nhanh vào những tài nguyên sử dụng lại liên tục (tương tự khái niệm cache).

* Phần việc swapping/overlaying giữa 2 cấp của bộ nhớ được hệ thống hardware thực thi tự động dựa trên nhu cầu (fetching-on-demand scheme). Khi có một truy cập vào 'ô nhớ' ko chứa trong memory, thì hệ thống sẽ kích hoạt quá trình thay thế dữ liệu, giữa memory và storage.

*Concept của Güntsch, dù mang tính cách tân, đột phá nhưng chưa bao giờ được thực hiện, chiếc máy mà ông mô tả chưa bao giờ được xây dựng nên. Không lâu sau đó, chiếc siêu máy tính Atlas khai sinh ra Virtual Memory - một phiên bản hiện thực hoá hoàn hảo hơn cả ý tưởng của Güntsch*

---

## 3. Virtual Memory Implementation: Atlas, Multics, Burroughs

Siêu máy tính [Atlas](https://history-computer.com/ModernComputer/Electronic/Atlas.html) được phát triển trong khoảng 1956-1962, được xem là chiếc computer đầu tiên sở hữu bộ nhớ ảo - Virtual Memory. Kiến trúc Virtual Memory của Atlas cũng xoay quanh mô hình Güntsch, gồm 3 thành phần chính:

1. **Address Translation Hardware** - Có chức năng biên dịch địa chỉ bộ nhớ ảo (Virtual Address) thành địa chỉ bộ nhớ vật lý tương ứng (physical address). Traslation Hardware vẫn được sử dụng phổ biến trên kiến trúc máy tính hiện đại, dưới tên gọi: [MMU - Memory Management Unit](https://en.wikipedia.org/wiki/Memory_management_unit).

2. **Page Fault Technique** - Là kỹ thuật cập nhật page dữ liệu còn thiếu lên Memory và update bảng tham chiếu trong trường hợp Translation Hardware ko tìm thấy tham chiếu đến Physical Address. Atlas cũng là cỗ máy đầu tiên giới thiệu thuật ngữ [Paging](https://en.wikipedia.org/wiki/Paging).

3. **Page Replacement Algorithm** - Một giải thuật áp dụng cho trường hợp physical memory quá tải và cần giải phóng bớt vùng nhớ ít sử dụng.

> Atlas has memory of 16K words, 48bits/word (96KB Memory)

*Nếu muốn tìm hiểu sâu hơn về kiến trúc của Atlas, chư vị đại hiệp có thể đọc thêm về Atlas Supervisor và Atlas Hardware ở [đây](http://www.chilton-computing.org.uk/acl/technology/atlas/p019.htm). Còn dưới đây là hình ảnh mô tả MMU*

![MMU principle](/assets/images/640px-MMU_principle_updated)

Những thế hệ computer kế thừa Atlas càng hoàn thiện hơn công nghệ lưu trữ và quản lý bộ nhớ, đáng kể nhất là Multics và Burroughs. 2 hệ máy này đi kèm với những đột phá đi-trước-thời-đại như Multiprocessing/Multitasking, Dynamic Linking, Hierarchical file system... đã làm tiền đề và nguồn cảm hứng cho toàn bộ hệ điều hành sau này như Unix và Windows.

---

## 4. Single-level store and Memory-map

Với nền tảng của 3 chiếc máy huyền thoại, computer đã dần trở nên "lỗi lạc" hơn:

* Có thể thực thi đa nhiệm và sử dụng bộ nhớ với hiệu suất cao nhất, cho phép dùng nhiều Memory hơn cả số Memory vật lý thực.

* Operating System đời mới còn đảm nhiệm luôn công việc swap-in/swap-out Memory blocks,vốn là việc rất khó khăn và mất thời gian với một lập trình viên.

Có thể nói, lý thuyết Single-level Store đã được thể hiện đầy đủ nhất trên hệ máy Multics. Bộ nhớ ảo của Multics được triển khai kèm công nghệ phân mảnh bộ nhớ và kho lưu trữ. Xem dữ liệu là những mảnh bytes thuần tuý, và Operating System phải có nhiệm vụ phân mảnh, quản lý, tham chiếu, đặc biệt là phải giúp process ghi và đọc lên những mảnh bytes này.

*Với database, phần đa số vẫn chọn Disk làm nơi lưu trữ và dùng RAM để thực thi chương trình, chủ yếu là do Price và Volatile. Cũng có một số DBMS hoạt động hoàn toàn trên RAM và tự tin rằng với công nghệ hiện tại, Volatile ko còn là vấn đề nữa mà chỉ tồn tại lý do duy nhất để ko lưu data trên RAM là Price mà thôi.*

### Vậy memory-map hoạt động như thế nào?

Mmap() là hàm chức năng của hệ thống mà hầu hết OS, chuẩn POSIX hay Windows đều hỗ trợ. Mmap() khi được gọi sẽ tạo ra tham chiếu (mapping) giữa tập tin nguồn và bộ nhớ. Việc mapping này được thực thi tại bộ nhớ ảo của Process.

Từ lúc mapping thành công trở đi, công đoạn quản lý quá trình chia vùng nhớ, bảng địa chỉ tham chiếu, tải nội dung lên RAM, lưu nội dung xuống file, giải phóng bộ nhớ trống... những công việc khó khăn, được nhân hệ điều hành (Kernel) gánh vác hết.

Có 2 kiểu mapping chính là file-backed và anonymous, khác biệt giữa chúng là dữ liệu sau khi đc mapping có lưu lại xuống file hay xoá sổ hoàn toàn.

Ngoài ra tôi tìm được series youtube giải thích rất hay và rõ ràng về công nghệ virtual memory, tác giả kênh yt là [David Black-Scaffer](https://www.youtube.com/channel/UCzf_XjIoKSf4Ve2fH7xn-3A/feed)
https://www.youtube.com/playlist?list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX

---

## 5. The Lightning Database

### Inherit from Single-Level Store

Lightning được phát triển dựa trên concept của Single-level store

### Born from Berkerley Database - BDB

Cải tiến từ Berkerley Database để khắc phục những khuyết điểm của người tiền nhiệm này.


# Reference

https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=1369143

https://history-computer.com/ModernComputer/Electronic/Atlas.html

https://multicians.org/features.html

https://multicians.org/multics-vm.html

http://www.chilton-computing.org.uk/acl/technology/atlas/p019.htm

https://en.wikipedia.org/wiki/Translation_lookaside_buffer

https://www.kernel.org/doc/gorman/

http://www.lmdb.tech/doc/

https://symas.com/lmdb/technical/

https://stackoverflow.com/questions/9414565/understanding-virtual-address-and-virtual-address-space