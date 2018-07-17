---
layout: post
title: "Ouroboros: A Provably Secure Proof-of-Stake Blockchain Protocol"
comments: true
description: "Ouroboros - Một giao thức tín nhiệm chuỗi"
keywords: "blockchain, proofofstake, cardano, ouroboros"
---

Một paper được dịch và tổng hợp từ White paper Cardano SL:
https://iohk.io/research/papers/#9BKRHCSI

Tác giả: Aggelos Kiayias, Alexander Russell, Bernardo David, Roman Oliynykov

Qua bài nghiên cứu, nhóm tác giả giới thiệu "Ouroboros", giao thức blockchain đầu tiên trên nền tảng "Proof-of-Stake" (băng chứng cổ phần) đảm bảo tính bảo mật nghiêm ngặt.

Ouroboros được bổ sung thêm các tính chất bảo mật và cải thiện hiệu suất so với giao thức bitcoin hiện tại (nền tảng Proof of Work). Ngoài ra, Ouroboros cũng đưa đến hệ thống chia thưởng tài nguyên cân bằng hơn.

Và cuối cùng, nhóm tác giả cũng giới thiệu những thực nghiệm đầu tiên của protocol này bằng xử lý và xác nhận các giao dịch trong thực tế.

# 1. Introduction

Trở lại với giao thức Proof-of-Work mà bitcoin đang sử dụng, nguyên lý cho sự hoạt động của giao thức này là năng lượng cần để đáp ứng cho sự thực thi. Tại thời điểm viết bài, năng lượng cần thiết để tạo ra 1 block mới trong chuỗi blockchain sẽ tiêu tốn tương đương năng lượng cung cấp cho 1 quốc gia nhỏ.

Vấn đề năng lượng này chính là động lực cho những nghiên cứu về các giao thức mới tối ưu hơn về hiệu năng để thay thế giao thức Proof of Work. Một điểm cần lưu ý là cơ chế chia phần của Proof of Work là sự chỉ định ngẫu nhiên các "thợ đào" (miner) dựa trên năng lực tính toán của họ (miner).

Với giao thức dạng Proof of Stake, công việc và phần thưởng được chỉ định ngẫu nhiên dựa vào tỉ lệ đóng góp của mỗi cổ đông (stakeholder). Tỉ lệ cổ phần này được ghi trong sổ cái. Ý tưởng này có vẻ rất khả thi nhưng để hiện thức hóa được nó thì có rất nhiều thử thách về kĩ thuật, phân tích, định nghĩa cần được giải quyết.

**Previous Work:**

Khái niệm về giao thức Proof of Stake thật ra đã được đưa ra thảo luận và tranh cãi rất nhiều trên các diễn đàn về bitcoin. Một số loại tiền mã hóa cũng đã áp dụng/triển khai giao thức PoS. Nhưng nhìn chung giao thức PoS lúc này vẫn chưa đảm bảo hoàn toàn về các khía cạnh bảo mật.

Ngoài ra một số các giao thức khác cũng được đưa ra, cũng với mục tiêu thay thế các giao thức Proof of Work như: Proof of Space, Proof of Space-time. Nhưng dường như những loại giao thức này vẫn yêu cầu một hệ thống hạ tầng đắt đỏ (về cả khía cạnh lưu trữ lẫn năng lực tính toán).


**The PoS Design Challenge**

Vấn đề cơ bản nhất mà giao thức PoS cần giải quyết là quá trình chỉ định, phân công công việc và phần thưởng. Để đạt được sự công bằng trong quá trình chỉ định ngẫu nhiên giữa các cổ đông, "entropy" phải được đưa vào hệ thống, và cơ chế đưa ra entropy có thể sẽ bị thao túng bởi 1 nhóm đối tượng.

Entropy: Mức độ biến động (hỗn loạn) của thông tin khi nhân một tin hiệu từ sự kiện ngẫu nhiên.
https://en.wikipedia.org/wiki/Entropy_(information_theory)

Ví dụ, khi một nhóm cổ đông có thể giả lập để thực hiện một giao thức để tìm ra một sự tiếp diễn giữa các nhóm cổ đông chung mục đích (xấu), như vậy họ sẽ thành lập đc một liên minh thao túng quá trình chỉ định. Đây là nhược điểm được biết đến với tên "grinding" (vulnerability)

**Our results**

Nhóm tác giả giới thiệu Ouroboros, một hệ thống Proof of Stake được đảm bảo an toàn.

