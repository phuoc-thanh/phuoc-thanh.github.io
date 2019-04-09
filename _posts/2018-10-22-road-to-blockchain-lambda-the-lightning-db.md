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

Một câu hỏi tuy đơn giản nhưng sâu sắc.

..

## 1. Computer Memory & Storage

Trước hết, chúng ta cùng xem lại các qui chuẩn về bộ nhớ, lưu trữ của máy tính.

**Computer có những hình thức lưu trữ nào?**

Đa phần những ghi chép và nghiên cứu trong ngành khoa học máy tính cho rằng Computer có 2 vùng lưu trữ chính là Main Memory và Secondary Storage, cũng có thể gọi tên phân biệt là "bộ nhớ" và "kho lưu trữ". Ngoài ra, những chíp vi xử lý mới còn có thêm bộ nhớ đệm (L1-L2-L3 Cache) cũng làm phần việc tương tự như Main Memory tuy nhiên dung lượng của Cache Mem rất nhỏ và ko nằm trong tầm quan sát/kiểm sát của người sử dụng.

* Main/Primary Memory: Theo kiến trúc von Neumann thì Main Memory là nơi chứa các tập lệnh (instructions) và dữ liệu (data) dành cho sự truy cập tức thời của CPU. RAM - như các bạn biết, là Memory của những chiếc PC hiện tại.

* Secondary Storage: Tất cả những nơi lưu trữ còn lại ngoài Main Memory thì được xếp vào Secondary Storage. Hard Disk Drive, Solid-state Drive là phần cứng lưu trữ phổ biến nhất hiện nay, được xem là Secondary Storage.

**Vậy dữ liệu nên được lưu ở đâu?**

RAM hay Disk đều có thể trở thành nơi lưu trữ dữ liệu, ltv có toàn quyền lựa chọn địa điểm lưu trữ, định dạng dữ liệu, và cả cách thức lưu trữ. Chọn Ram hay Disk, đều có những ưu điểm, nhược điểm riêng, tốc độ thường đi đôi với rủi ro và chi phí.

Vì giá thành quá cao so với Disk Storage và tính chất volatile (Ko có điện, mất hết data) của RAM Memory, nên dữ liệu thường được ưu tiên lưu trên Disk, phần dữ liệu sử dụng thường xuyên hoặc những tác vụ đặc biệt thì lưu trên RAM .

Nhưng có thể ko phải ai cũng biết, còn có một cách lưu trữ ít nổi tiếng hơn, tên gọi là memory-map, sử dụng cả RAM lẫn Disk để phục vụ cho công việc đọc/ghi dữ liệu.

---

## 2. Virtual Memory & Single-level Store

Ở những thế hệ computer đầu tiên trên thế giới, sự phân cấp bộ nhớ trong một máy tính rất rõ ràng, rành mạch, khi đó, Main/Primary Memory và Secondary Storage còn có tên gọi là bộ nhớ sơ cấp và bộ nhớ thứ cấp.

Các nhà khoa học máy tính đã trải qua chặng đường dài với rất nhiều nỗ lực xoá nhoà ranh giới phân biệt giữa 2 cấp bộ nhớ này, và công nghệ được tạo ra sau cùng là Virtual Memory. Cá nhân tôi nghĩ, đây là phát minh quan trọng bậc nhất trong ngành KHMT.

### 2.1 Khơi nguồn của bộ nhớ ảo

Những 40-50, với sự tồn tại của 2 cấp bộ nhớ kèm theo hạn chế của Memory, lập trình viên phải đảm nhiệm một công việc quan trọng là lên kế hoạch và tính toán các bước luân chuyển của dữ liệu giữa 2 cấp bộ nhớ. Công việc này chủ yếu là chia bộ nhớ ra thành từng blocks (về sau gọi là segments và pages), và tính toán thay đổi nơi lưu trữ của những block này (swap / overlay works).

Năm 1956, nhà Vật Lý học người Đức **Fritz-Rudolf Güntsch**, trong luận án tiến sĩ của mình, đã mô tả chiếc máy tính có khả năng tự điều chỉnh vùng nhớ - một cách tự động hoàn toàn.

Dựa trên bộ nhớ nhanh nhất thời điểm đó - lõi nhớ của siêu máy tính Whirlwind, ông lên ý tưởng chia bộ nhớ sơ cấp thành 6 blocks, mỗi block có dung lượng 100-words. Bộ nhớ này được sử dụng cùng với vùng tham chiếu địa chỉ (Address Space). Address Space có không gian tối đa là 1000 blocks, mỗi block cũng mang dung lượng 100-words.

Hình mô tả mô hình máy tính Güntsch:

![Güntsch’s virtual memory concept](/assets/images/1956_vm_concept.png)

* 6 blocks của Memory lần lượt chứa instructions ở 2 blocks M1, data ở 2 blocks M2, và vùng nhớ cố định ở 2 blocks M3 - là nơi được sử dụng để access nhanh vào những tài nguyên sử dụng lại liên tục (tương tự khái niệm cache).

* Phần việc swapping/overlaying giữa 2 cấp của bộ nhớ được hệ thống hardware thực thi tự động dựa trên nhu cầu (fetching-on-demand scheme). Khi có một truy cập vào 'ô nhớ' ko chứa trong memory, thì hệ thống sẽ kích hoạt quá trình thay thế dữ liệu, giữa memory và storage.

*Concept của Güntsch, dù mang tính cách tân, đột phá nhưng chưa bao giờ được thực hiện, chiếc máy mà ông mô tả chưa bao giờ được xây dựng nên. Không lâu sau đó, chiếc siêu máy tính Atlas khai sinh ra Virtual Memory - một phiên bản hiện thực hoá hoàn hảo hơn cả ý tưởng của Güntsch*

### 2.2 Atlas, Multics và Single-level store

Siêu máy tính [Atlas](https://history-computer.com/ModernComputer/Electronic/Atlas.html) được phát triển trong khoảng 1956-1962, được xem là chiếc computer đầu tiên mang trong mình một bộ nhớ ảo (Virtual Memory)

Chính những ý tưởng tiên phong của **Güntsch** đã thúc đẩy những nhà thiết kế Atlas đem đến bộ nhớ ảo hoàn thiện gồm:

1. Translation Hardware: Tương ứng với [MMU](https://en.wikipedia.org/wiki/Memory_management_unit) trong kiến trúc máy tính hiện đại. Tự động biên dịch địa chỉ từ chương trình (hay từ processor đem đến) thành địa chỉ bộ nhớ vật lý (physical address). Khi một địa chỉ ko được tìm thấy bởi translation software, nó sẽ raise một page fault exception và gọi đến handling tương ứng được cung cấp bởi OS.

2. Paging technique: Chia bộ nhớ thành những 'page' nhỏ hơn, để tạo điều kiện cho qua trình chuyển đổi nơi lưu trữ của dữ liệu, từ bộ nhớ sơ cấp sang thứ cấp (from memory to storage)

Non-equivalence interruption handling(về sau gọi là Page fault): Hoạt động của Atlas Supervisor khi chuyển dữ liệu từ storage vào memory hay còn gọi là swap-in data lên memory khi chương trình request một blocks chưa có trong mem.

3. Page Replacement Algorithm: Khi physical memory đã sử dụng hết thì OS cung cấp cơ chế giải phóng vùng nhớ ít sử dụng.

* Máy Whirlwind có memory 2K words, 16bits/word ~ 4KB Memory

* Máy Atlas có memory 16K words, 48bits/word ~ 96KB Memory

Page of 512 words (3072 Bytes), core mem ~ 32pages, fixed mem ~ 16pages, sub mem 2pages

[Kiến trúc Virtual Address Space của Windows](https://docs.microsoft.com/en-us/windows/desktop/memory/virtual-address-space)


### 2.2 Lưu trữ đơn cấp: Single-level store
Dựa trên một công nghệ cũ là Single-level store được giới thiệu cùng với sự xuất hiện của cỗ máy [Multics](http://gunkies.org/wiki/Multics) huyền thoại.

Bàn về lý thuyết của SLS trước nhé.

Ở trên tôi có đưa ra vấn đề là máy tính có rất nhiều nơi lưu trữ và ltv cần đưa ra quyết định chọn nơi nào để lưu.

---

## 3. Memory-map files

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

## The Lightning Database

### Inherit from Single-Level Store

Lightning được phát triển dựa trên concept của Single-level store

### Born from Berkerley Database - BDB

Cải tiến từ Berkerley Database để khắc phục những khuyết điểm của người tiền nhiệm này.


# Reference

https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=1369143

https://history-computer.com/ModernComputer/Electronic/Atlas.html

http://www.chilton-computing.org.uk/acl/technology/atlas/p019.htm

https://www.kernel.org/doc/gorman/

http://www.lmdb.tech/doc/

https://symas.com/lmdb/technical/

https://stackoverflow.com/questions/9414565/understanding-virtual-address-and-virtual-address-space