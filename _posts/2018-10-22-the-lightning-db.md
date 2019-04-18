---
layout: post
title: "The Lightning Database"
comments: true
description: "The Lightning Database - Part 1"
keywords: "blockchain, lambda, LMDB, Lightning, Memory-Mapped, database, memory"
---

Khi khởi động một dự án, ở giai đoạn thiết kế tổng thể cấu trúc hệ thống, khâu quyết định công cụ lưu trữ dữ liệu thường bị xem nhẹ và diễn ra cũng rất nhanh gọn. Chúng ta mặc định trong đầu những lựa chọn khá hạn chế xung quanh SQL / NoSQL, và ko nghĩ rằng sự lựa chọn đó đòi hỏi phức tạp hay khó khăn. MySQL, MsSQL, MongoDb, SQL Lite, Redis.. cứ thế mà pick, gần như chỉ dựa trên yếu tố "quen tay".

Liệu có một lúc nào đó, khi không có áp lực nào thúc ép, tính hiếu kỳ có gây cảm hứng cho một lập trình viên bình thường suy nghĩ về CSDL (Database) theo cách khác thường?

Computer là cỗ máy có nhiều loại bộ nhớ và nơi lưu trữ khác nhau, vậy những MySQL, Redis, Mongodb mà chúng ta vẫn hay sử dụng lưu dữ liệu ở đâu? Trên Disk, trên RAM, hay.. CPU Cache-Mem?


---

## 1. Computer Memory & Storage

Tính hiếu kỳ, đối với lập trình viên có thể ko giúp ích nhiều trong công việc thường nhật, nhưng theo tôi thì nó cần thiết để trở thành lập trình viên ko-bất-tài. Hôm nay tính hiếu kỳ với cụm từ "Single-level Store" thôi thúc tôi tìm hiểu bản chất công nghệ lưu trữ của computer. Dù chỉ là một phần nhỏ của lịch sử máy tính, nhưng vô cùng thú vị.

### Computer có những hình thức lưu trữ nào?

Đa phần những ghi chép và nghiên cứu trong ngành khoa học máy tính cho rằng Computer có 2 vùng lưu trữ chính là Main Memory và Secondary Storage, cũng có thể gọi tên phân biệt là "bộ nhớ" và "kho lưu trữ".

* Main/Primary Memory: Theo kiến trúc von Neumann thì Main Memory là nơi chứa các tập lệnh (instructions) và dữ liệu (data) dành cho sự truy cập tức thời của CPU. RAM - như các bạn biết, là Memory của những chiếc PC hiện tại.

* Secondary Storage: Tất cả những nơi lưu trữ còn lại ngoài Main Memory thì được xếp vào Secondary Storage. Hard Disk Drive, Solid-state Drive là phần cứng lưu trữ phổ biến nhất hiện nay, được xem là Secondary Storage.

*Những chíp vi xử lý mới còn có thêm bộ nhớ đệm (L1-L2-L3 Cache) cũng làm phần việc tương tự như Main Memory tuy nhiên dung lượng của Cache Mem rất nhỏ và ko nằm trong tầm quan sát/kiểm sát của người sử dụng.*

![magnetic drum](/assets/images/lmdb/drum.jpg)

Ảnh trên là một "bộ nhớ" đời đầu của Computer, còn được nhớ đến với tên gọi Magnetic Drum.

### Vậy dữ liệu được lưu ở đâu?

RAM hay Disk đều có thể trở thành nơi lưu trữ dữ liệu, ltv có toàn quyền lựa chọn địa điểm lưu trữ, định dạng dữ liệu, và cả cách thức lưu trữ. Chọn Ram hay Disk, đều có những ưu điểm, nhược điểm riêng, tốc độ thường đi đôi với rủi ro và chi phí.

Vì giá thành quá cao so với Disk Storage và tính chất "Volatile" (Ko có điện, mất hết data) của RAM Memory, nên dữ liệu thường được ưu tiên lưu trên Disk, phần dữ liệu sử dụng thường xuyên hoặc cần thiết để thực thi tiến trình (process) thì lưu trên RAM.

Ngay cả với khu vực database, đa số hệ quản trị dữ liệu (DBMS) cũng chọn Disk làm nơi lưu trữ và dùng RAM để thực thi chương trình, vẫn là lý do Price & Volatile. Cũng có một số DBMS hoạt động hoàn toàn trên RAM và tự tin rằng với hạ tầng thông tin hiện tại, Volatile ko còn là vấn đề nữa mà chỉ tồn tại lý do duy nhất để ko lưu data trên RAM, là Price mà thôi.

Tuy nhiên có thể ko phải ai cũng biết, còn có một cách lưu trữ ít nổi tiếng hơn, sử dụng cả RAM lẫn Disk để phục vụ cho công việc đọc/ghi dữ liệu. Cách lưu trữ đó có nguồn gốc từ Virtual Memory và Single-Level Store Concepts, mà sau đây chúng ta sẽ tìm hiểu.


---

## 2. Virtual Memory Concept

Những năm 40-50, chính vì hạn chế về dung lượng Memory, lập trình viên khi đó phải đảm nhiệm một công việc quan trọng là lên kế hoạch và tính toán các bước luân chuyển của dữ liệu giữa 2 cấp bộ nhớ là Memory và Storage. Công việc này chủ yếu là chia bộ nhớ ra thành từng blocks (về sau gọi là segments và pages), và tính toán kế hooạch di chuyển những block này giữa 2 cấp bộ nhớ (swap / overlay works).

Để tăng hiệu suất sử dụng của bộ nhớ và tận dụng tốt hơn nguồn tài nguyên của computer, các nhà khoa học máy tính đã nỗ lực tìm cách xoá đi ranh giới phân biệt giữa 2 cấp bộ nhớ này, và công nghệ được tạo ra sau cùng là Virtual Memory - phát minh quan trọng bậc nhất trong ngành KHMT.

### Lý thuyết bộ nhớ ảo

Năm 1956, nhà Vật Lý học người Đức **Fritz-Rudolf Güntsch**, trong luận án tiến sĩ của mình, đã mô tả chiếc máy tính có khả năng tự điều chỉnh vùng nhớ - một cách tự động hoàn toàn.

Dựa trên bộ nhớ nhanh nhất thời điểm đó - lõi nhớ của siêu máy tính Whirlwind, ông lên ý tưởng chia bộ nhớ sơ cấp thành 6 blocks, mỗi block có dung lượng 100-words. Bộ nhớ này được sử dụng cùng với vùng tham chiếu địa chỉ (Address Space). Address Space có không gian tối đa là 1000 blocks, mỗi block cũng mang dung lượng 100-words.

> At that time, Whirlwind has a memory of 2K words, 16bits/word (4KB Memory).

Mô hình máy tính Güntsch:

![Güntsch’s virtual memory concept](/assets/images/lmdb/1956_vm_concept.png)

* 6 blocks của Memory lần lượt chứa instructions ở 2 blocks M1, data ở 2 blocks M2, và vùng nhớ cố định ở 2 blocks M3 - là nơi được sử dụng để access nhanh vào những tài nguyên sử dụng lại liên tục (tương tự khái niệm cache).

* Phần việc swapping/overlaying giữa 2 cấp của bộ nhớ được hệ thống hardware thực thi tự động dựa trên nhu cầu (fetching-on-demand scheme). Khi có một truy cập vào 'ô nhớ' ko chứa trong memory, thì hệ thống sẽ kích hoạt quá trình thay thế dữ liệu, giữa memory và storage.

*Concept của Güntsch, dù mang tính cách tân, đột phá nhưng chưa bao giờ được thực hiện, chiếc máy mà ông mô tả chưa bao giờ được xây dựng nên. Không lâu sau đó, siêu máy tính Atlas khai sinh ra Virtual Memory - hiện thực hoá ý tưởng của Güntsch*


---

## 3. Single-Level Store Concept

Vậy lý thuyết của Güntsch được hình thành và phát triển như thế nào?

### Hiện thực hoá Virtual Memory

[Atlas](https://history-computer.com/ModernComputer/Electronic/Atlas.html) được phát triển trong khoảng 1956-1962, là chiếc computer đầu tiên sở hữu bộ nhớ ảo - Virtual Memory. Kiến trúc Virtual Memory của Atlas cũng xoay quanh mô hình Güntsch, gồm 3 thành phần chính:

1. **Address Translation Hardware** - Có chức năng biên dịch địa chỉ bộ nhớ ảo (Virtual Address) thành địa chỉ bộ nhớ vật lý tương ứng (physical address). Translation Hardware vẫn được sử dụng phổ biến trên kiến trúc máy tính hiện đại, dưới tên gọi: [MMU - Memory Management Unit](https://en.wikipedia.org/wiki/Memory_management_unit).

2. **Page Fault Technique** - Là kỹ thuật cập nhật page dữ liệu còn thiếu lên Memory và update bảng tham chiếu trong trường hợp Translation Hardware ko tìm thấy tham chiếu đến Physical Address. Atlas cũng là cỗ máy đầu tiên giới thiệu thuật ngữ [Paging](https://en.wikipedia.org/wiki/Paging).

3. **Page Replacement Algorithm** - Một giải thuật áp dụng cho trường hợp physical memory quá tải và cần giải phóng bớt vùng nhớ ít sử dụng.

> Atlas has memory of 16K words, 48bits/word (96KB Memory) at that time.

*Chi tiết hơn về kiến trúc Atlas Supervisor và Atlas Hardware bạn có tham khảo thêm ở [link này](http://www.chilton-computing.org.uk/acl/technology/atlas/p019.htm). Còn dưới đây là hình mô tả tương tác của MMU với CPU và Memory*

![MMU principle](/assets/images/lmdb/640px-MMU_principle_updated.png)

Những thế hệ computer kế thừa Atlas càng hoàn thiện hơn công nghệ ảo hoá bộ nhớ, đáng kể nhất là Multics và Burroughs. 2 hệ máy này đi kèm với những đột phá đi-trước-thời-đại như Multiprocessing/Multitasking, Dynamic Linking, Hierarchical file system... đã làm tiền đề và nguồn cảm hứng cho toàn bộ hệ điều hành sau này gồm cả Unix, Windows.

### Hiện thực hoá Single-level Store

Với nền tảng công nghệ của 3 chiếc máy huyền thoại, computer dần trở nên "lỗi lạc" hơn:

* Có thể thực thi đa nhiệm và sử dụng bộ nhớ với hiệu suất cao nhất, cho phép dùng nhiều Memory hơn cả số Memory vật lý thực.

* Operating System có khả năng đảm nhiệm công việc swap-in/swap-out Memory blocks, vốn là việc rất khó khăn và mất thời gian với một lập trình viên.

Đáng lưu ý nhất, lý thuyết Single-level Store cũng được hoàn thiện trên hệ máy Multics cùng với mô hình Persistent Object & Mapping mà nó giới thiệu.

Bộ nhớ ảo của Multics được triển khai bằng cách phân mảnh Memory và Storage. Xem dữ liệu chỉ đơn giản là những mảnh bytes thuần tuý, Operating System có nhiệm vụ phân mảnh, quản lý, tham chiếu, đặc biệt là giúp program đọc/ghi lên những mảnh bytes này. Program lúc này chỉ cần read/write thẳng vào phần bộ nhớ được map đó trên Virtual Memory. Đó cũng là cách mà memory-mapped files/mmap hoạt động.

*Video Series Bonus below: dành cho ai có ý muốn hiểu sâu hơn về virtual memory*

*[David Black-Scaffer - Virtual Memory](https://www.youtube.com/playlist?list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX)*


---

## 4. The Lightning Database

Lightning (hay LMDB) với tên gọi đầy đủ: Lightning Memory-Mapped Database - là một CSDL dạng Key-Value được viết bởi Howard Chu tại Symas, ra mắt năm 2011. Lightning có thiết kế kỹ thuật ảnh hưởng lớn từ Berkeley DB cùng nhiều bổ sung quan trọng.

### Triết lý thứ nhất: Single-Level Store (SLS)

Lightning được phát triển dựa trên concept Single-level store trên chiếc máy Multics, đi tìm một hướng lưu trữ thuần tuý nhất, hoàn toàn bỏ qua Type & Structure của dữ liệu mà hướng đến cấu trúc thông tin thô nhất: những mảnh bytes.

Toàn bộ file data của Lightning trên Disk sẽ được map vào Memory thông qua mmap(), sau đó hành động read/write được thực thi thẳng vào Mapped-Files ở Virtual Address. API của Lightning còn cho phép truy vấn, cập nhật dữ liệu dạng pointer-based Object, nghe hấp dẫn quá phải ko?

Lợi ích chính mà SLS và Mmap mang lại, là khả năng bỏ qua cache, buffer, memcpy. Đây là điểm mấu chốt khiến Lightning có thể sử dụng Memory với mức hiệu quả tối đa, read/write performance nhờ đó mà cải thiện rất rất nhiều.

### Triết lý thứ hai: Multiversion Concurrency Control (MVCC)

Một điểm nổi bật nữa của LMDB là triển khai MVCC, điều này có nghĩa là gì?

[MVCC](https://en.wikipedia.org/wiki/Multiversion_concurrency_control) là một trong những phương pháp kiểm soát tính đồng thời (Concurrency & Multithreading), điểm đặc biệt nhất của MVCC là Isolation. Tôi ko thể tìm được từ tiếng Việt sát nghĩa cho ngữ cảnh 'Isolation' ở đây, nhưng có thể giải thích đơn giản như khả năng cung cấp góc nhìn độc lập đối với dữ liệu giữa các nguồn truy cập đồng thời (multiple threads or processes).

MVCC đảm bảo mỗi thread truy cập vào DB sẽ luôn lấy được một view từ dữ liệu "cập-nhật-nhất" mà ko phải chờ đợi hành động modify nào khác. Sự đảm bảo này được thực hiện bằng kỹ thuật copy-on-write, khi cần thiết phải modify dữ liệu, một phiên bản copy mới của DB sẽ được tạo ra, dành riêng cho việc modify, dữ liệu thực sẽ ko bao giờ bị ghi đè - overwritten.

Cũng phải nói thêm là khi nhắc tới chiến thuật copy-on-write hay snapshot isolation, lợi ích lớn nhất nó mang lại là tăng cường độ tin cậy (Reliability) cho DB, dữ liệu nằm trong DB sẽ ko bao giờ bị xung đột hay mất mát. Tất nhiên, đi kèm theo lợi ích đó là cái giá đắt đỏ phải trả đối với tài nguyên máy. Cực kỳ hao tốn và nhanh chóng nuốt sạch dung lượng kho lưu trữ là điều phải cân nhắc.

Thậm chí việc dọn rác cũng sẽ tiêu tốn tài nguyên CPU/Memory rất nhiều nữa.

Và LMDB quyết định chỉ giữ 2 bản snapshot của DB, ngoại trừ long-live transaction được tác giả Howard Chu khuyên là nên tránh dùng đến.

### Điểm nổi trội của Lightning?

**Compact, Reliability, Performance là 3 điểm ăn-tiền của LMDB.**

* Dung lượng đóng gói của LMDB chỉ 40KB và nó có thể chạy trên các hệ điều hành chính gồm Linux, Windows, MacOS, Android, BSD, Solaris...

* Đã có nhiều bài test được thực hiện với LMDB về độ tin cậy, và gần như vẫn chưa tìm được failure case. Với chiến thuật copy-on-write như đã mô tả ở trên thì trường hợp xấu nhất có thể xảy ra ở LMDB là bị mất last transaction trong trường hợp cúp điện hay crash app.

* LMDB có tốc độ đọc/ghi xuất sắc, gần như vượt trội (Outperformed) các thể loại DB trong những lần benchmark, đặc biệt là ở khả năng Read và Batch-Write.

Dưới đây là một vài benchmark được trích từ slide của Howard Chu, có thể các bạn cho rằng như vậy thì ko khách quan, nhưng thật ra kết quả benchmark trên một API khác của Google cũng xác nhận tốc độ của LMDB vượt trội.

![loadtime](/assets/images/lmdb/benchmark01.png)

![WriteScale](/assets/images/lmdb/benchmark02.png)

![ReadScale](/assets/images/lmdb/benchmark03.png)


---

## 5. Next Things n References

Còn rất nhiều thứ để khám phá về LMDB như kiến trúc, ứng dụng, cách sử dụng... nhưng bài viết đã quá dài, nên tôi phải kết thúc vậy. Bên dưới đây là toàn bộ references mà bài viết sử dụng.


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