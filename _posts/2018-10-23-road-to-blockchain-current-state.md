---
layout: post
title: "Road to Blockchain: Current State of Blockchain"
comments: true
description: "Road to Blockchain: Real Power"
keywords: "blockchain, bitcoin, haskell, lambda, p2p network, LMDB, Lightning Memory-Mapped Db"
---

Blockchain có ứng dụng thực tế nào đáng giá chưa?

Đây có lẽ là vấn đề được quan tâm nhất của blockchain, tính ứng dụng của nó là hoài nghi và cũng là hi vọng lớn nhất.

Theo tôi, đã đi qua nhiều bài viết về blockchain, có một suy nghĩ rất đơn giản về tính ứng dụng của nó. Xếp theo mức độ đáp ứng của yêu cầu, nếu một vấn đề đòi hỏi cả 3 tính chất của blockchain thì nó chính là sự lựa chọn hoàn hảo.

Nếu vấn đề chỉ tận dụng đc 2/3 tính chất của blockchain, thì chọn blockchain để làm giải pháp cũng đc coi là một cách tiếp cận tốt.

Nhưng nếu chỉ cần 1 tính chất của blockchain, thì nó ko còn là bài toán blockchain nữa, nó sẽ chỉ là "distributed database", hay "consensus network" hay là immutable writing chain mà thôi..

## 3/3 Applications: Public Blockchain

Giao dịch tiền kỹ thuật số một cách ngang hàng chính là ứng dụng đầu tiên phải kể đến trong danh mục 3/3 của blockchain. Bitcoin có  một sổ cái giao dịch đồng bộ mà ai trong mạng lưới cũng có thể xem và tải về, sổ cái này được ghi liên tục dựa trên các thuật toán mã hoá để đảm bảo tính toàn vẹn. Và cuối cùng, ko ai thao túng được mạng lưới bitcoin, bởi cơ chế đồng thuận của nó. Nếu có sự thao túng đối với bitcoin, đó có lẽ là giá cả, vấn đề này nằm ngoài phạm vi của blockchain.

Hồ sơ công khai (Public held property records): Ai cũng có thể tải về, và mọi người đều xem được hồ sơ, yêu cầu tính minh bạch trong dữ liệu. Cơ chế đồng thuận có thể theo hướng đặc thù riêng. Như các dữ liệu sở hữu phương tiện giao thông.

Kho dữ liệu định danh (Identity Services): Dữ liệu cá nhân được phân tán dành cho các dịch vụ công của chính phủ

Tokenization of Assest: Tất cả tài sản qui ra thành một token để có thể dễ dàng giao dịch!

Public Election (Voting)


## 2/3 Applications: Private/Permissioned Blockchain

Một số giải pháp dựa trên nền tảng Integrity of Data, nhưng ledger lại nằm trên một mạng lưới ko ngang hàng (not peer-to-peer) và mỗi Node có vai trò khác nhau, quyền lực cũng phân tách. Bởi vì ko mang tính ngang hàng nên cơ chế đồng thuận cũng được triển khai theo cách khác, đa số đều loại bỏ "mining work".

Những chain kiểu này có thể kể đến như: An toàn thực phẩm, Truy xuất nguồn gốc, mạng lưới riêng tư của hệ thống doanh nghiệp xuyên quốc gia

## Deloitte's Global Blockchain Survey Report 2018 - Part 1

**Significant Advantages:** Lợi ích lớn nhất mà blockchain có thể mang lại so với hệ thống cũ: Tốc độ -> Hình thức hoạt động và nguồn lợi -> Bảo mật và rủi ro -> Chi phí.

**Organizational Barries** Rào cản lớn nhất đối với việc đầu tư vào công nghệ blockchain: Qui chế/Điều lệ -> Thay thế/Kế thừa hệ thống cũ -> Mối đe doạ về bảo mật -> Mơ hồ về lợi ích thu về (ROI) -> Thiếu hụt kỹ năng / hiểu biết của đội ngũ nội bộ.

**Consortium:** Có đến 74% tổ chức tham giagia cuộc khảo sát khẳng định rằng họ đang trong một liên minh/hiệp hội (consortium) sử dụng chung nền tảng blockchain hoặc họ đang rất muốn tham gia vào những hiệp hội như vậy.

**Blockchain Models:** Các hình thái blockchain đang được nhắm vào: Permissioned Blockchain (52%), Private Blockchain (44%), Public Blockchain (44%), Consortium (36%).

**Blockchain usecases:** Use case hiện tại của blockchain đang được phát triển, theo thứ tự giảm dần:
    Chuỗi cung ứng (Supply Chain)
    Internet of Things
    Danh tính số (Digital Identity)
    Số hoá sổ sách/ghi chép (Digital Records)
    Tiền số (Digital Currency)
    Thanh toán trực tuyến (Payments)
    Voting

Về thị trường tiềm năng, Trung Quốc đang cho thấy một nhu cầu rất cao đối với nhân lực và cũng đang đầu tư rất mạnh trong lĩnh vực Blockchain

![Nhu cầu nhân lực blockchain](/assets/images/blockchain/blockchain_hiring.png)

**Blockchain Journey** Hiện tại, mức độ thử nghiệm và đã đi vào hoạt động thực sự của các hệ thống blockchain đang được đẩy dần lên.

![Thực trạng blockchain](/assets/images/blockchain/blockchain_journey.png)


## Deloitte's Global Blockchain Survey Report 2018 - Part 2

**Financial Services**

Đây là lĩnh vực tiên phong, ảnh hưởng và triển vọng nhất đối với công nghệ BlockchainBlockchain. Blockchain và những ứng dụng từ sổ cái phân tán đang có tiềm năng rất lớn, và có khả năng tái định hình lại nền tảng tương tác giữa các tổ chức tài chính với khách hàng, hoặc giữa các mạng lưới tài chính. Có quá nhiều usecase mà blockchain đã và đang được ứng dụng trong lĩnh vực tài chính như: Thanh toán, Trao Đổi, GHi chép báo cáo giao dịch... Có thể nói cơ hội đang rộng mở đối với blockchain trong lĩnh vực này.

Về thách thức, blockchain được kỳ vọng giải quyết các bài toán:

    - Khả năng Mở Rộng (Scalability): Đây là điểm chính yếu mà các tổ chức kỳ vọng blockchain có thể mang đến cho họ một giải pháp
    - Tính bảo mật (Security): Đa phần (84%) đều tin rằng blockchain thực sự nâng tầm tính bảo mật của hệ thống, nhưng họ vẫn còn chưa nhận ra được mối nguy tiềm tàng sắp tới đối với blockchain.
    - Khởi tạo và hợp tác giữa các tổ chức trong liên minh: Đây là điều bắt buộc để có thể giải phòng toàn bộ tiềm năng của blockchain vào lĩnh vực.

**Life sciences & Healthcare**

Trong vòng 12 tháng qua, sự tham gia của công nghệ blockchain vào lĩnh vực khoa học sự sống (life science) và chăm sóc y tế (healthcare) thực sực gia tăng rất mạnh mẽ. Tuy vẫn có nhiều nghi hoặc về sự gián đoạn trong vận hành nếu áp dụng công nghệ mới, nhưng những doanh nghiệp vẫn ko muốn bị tụt lùi phía sau so với đối thủ và toàn bộ ngành công nghiệp y tế. Và họ tin rằng blockchain sẽ mang lại giá trị ở những mặt sau:

    - Giảm bớt sự phụ thuộc và chi phí quá cao cho các công tác trung gian bằng smart contracts và thành lập mạng lưới blockchain cho các bên tham gia. Ví dụ như quá trình thu thập và tổng hợp dữ liệu y tế, qui trình tiếp cận bệnh nhân, dịch vụ trung gian trong thanh toán hoá đơn y tế.
    - Tính minh bạch và khả năng thanh tra: Tăng cường sự trực quan trong các giao dịch giữa đối tác cùng một hệ sinh thái cũng là tăng mức độ hiệu quả trong vận hành. Hệ sinh thái đó có thể bao gồm viện nghiên cứu lâm sàng, doanh nghiệp dược phẩm, công ty thương mại...
    - Hợp tác về mặt dữ liệu: như hồ sơ y tế cá nhân, dữ liệu thử nghiệm lâm sàng, 
    - Mô hình kinh doanh mới dựa trên phân tách dữ liệu, riêng tư và có khả năng sinh lợi.

Mặc dù tất cả các dự án trong mảng khoa học sự sống đều đang ở bước sơ khai và thử nghiệm, nhưng cũng nhận đc sự đầu tư và hậu thuẫn rất lớn từ các đơn vị trong ngành, đây là tín hiệu thực sự khả quan.

**Public Sectors**

Khu vực hành chính công thông thường phản ứng khá chậm chạp với một công nghệ nổi lên nhanh như blockchain, và vài năm trở lại đây, một số cơ quan đã bắt đầu gỡ bỏ bức tường ngăn cách đó. Họ chuyển từ quan sát, hoài nghi tới thử nghiệm, và rồi bắt đầu có những suy nghĩ tích cực hơn, nghiêm túc hơn trong việc nghiên cứu và bắt đầu những chiến lược dài hạn.

Khi tương lai của blockchain được nhìn thấy, thì khả năng ứng dụng thực tế của blockchain có thể coi là "ko có giới hạn". Một số use case có thể kể ra như số hoá việc Định danh (Digital Identity), truy xuất nguồn gốc một số loại tài sản, bảo toàn dữ liệu..

Cuộc cách mạng blockchain đòi hỏi một sử cởi mở đối với sự thay đổi trong tổ chức, đó lại là một rào cản rất lớn đối với khu vực hành chính công. Những đòi hỏi khác biệt về sự riêng tư, bảo mật, và qui chế khiến các dịch vụ công rất khó thích ứng với blockchain. Đây là thử thách lớn, nhưng blockchain cũng ko phải chỉ nằm yên như vậy mà vẫn phát triển thay đổi, đa dạng hơn mỗi ngày, nên chúng ta vẫn có niềm tin vào nó.

**Technology, media & telecom**

Giữa lúc blockchain đang được thổi phồng và dấy lên nhiều hoài nghi, các doanh nghiệp thuộc khối này tiếp cận blockchain theo nhiều cách khác nhau.

Các nhà cung cấp tính toán đám mây (Cloud Computing Providers) đang thêm blockchain vào các dịch vụ của họ, doanh nghiệp sản xuất Vi xử lý cũng đã bán những sản phẩm chuyên dụng trong mục triển khai blockchain như card đồ hoạ ko có cổng tín hiệu, máy đào ASICS..

Doanh nghiệp viễn thông thì đang thử nghiệm các giải pháp blockchain, và mảng truyền thông giải trí cũng bắt đầu nghiên cứu và có một số sản phẩm thử nghiệm riêng như blockchain-based games, blockchain-based content..

Theo báo cáo của Deloitte, có tới 68% tổ chức/doanh nghiệp tin rằng họ sẽ đánh mất lợi thế nếu như ko nhanh chóng đầu tư vào công nghệ blockchain. Đối thủ của họ sẽ tìm cách cạnh tranh trực tiếp trên những giá trị mà  blockchain mang lại cho người dùng như sự minh bạch và mức độ tin tưởng.

Thực tế các doanh nghiệp công nghệ vẫn sẽ tiếp tục theo đuổi nền tảng blockchain trong thời gian tới. 

Đối với dịch vụ truyền thông, blockchain có thể giúp theo dõi và sinh lời từ nội dung số, giải quyết vấn đề bản quyền, quản lý nội dung số giữa tác giả và người dùng.

Đối với ngành viễn thông, blockchain có thể được ứng dụng làm hệ thống thanh toán giảm tránh gian lận, nó còn có thể ứng dụng trong việc lưu dữ liệu phân tán phục vụ cho kế toán và kiểm toán


## Potential cases

[Private Content]

## Reference

https://www2.deloitte.com/content/dam/Deloitte/us/Documents/financial-services/us-fsi-2018-global-blockchain-survey-report.pdf