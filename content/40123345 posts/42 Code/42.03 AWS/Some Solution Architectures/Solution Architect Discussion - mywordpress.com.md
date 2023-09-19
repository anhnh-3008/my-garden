---
title: "🌱 Solution Architect Discussion - mywordpress.com"
tags: [aws, architecture]
date: 2023-03-12
---

## 🌿Đề bài
- Một website viết blog
- Yêu cầu phải show được ảnh, content của các bài blog cho các users.
- Có khả năng scale
- Toàn bộ thông tin về users hay các blogs sẽ đươc lưu trong MySQL.

## 🌿 Kiến trúc áp dụng
![[00 Meta/01 Attachments/Pasted image 20230312230204.png]]
- Vẫn kiến trúc cũ như **theclothes.com**, nhưng web không cần lưu thông tin trạng thái giỏ hàng nên không cần sử dụng **ElastiCache**.
- Thay **RDS -> Aurora**, scale tốt hơn, performance tốt hơn, khả năng read scale tốt gấp 3 lần.(option tham khảo, dùng RDS thì cũng không sao, chi phí thấp hơn, tương đương với hiệu suât cũng thấp hơn thôi)

![[00 Meta/01 Attachments/Pasted image 20230312230434.png]]
- Về vụ lưu ảnh, nếu dự án chỉ có một **EC2 Instance**, không mở rộng thì lưu luôn vào **EBS - Elastic Block Store** thì cũng được. Cơ mà lúc scale thêm một instance thì kèm với đó là một **EBS mới**. Lúc gửi ảnh vào **EBS cũ** xong lúc sau **ELB** định tuyến qua **EBS mới** thế là mất ảnh.
- Để tránh tình trạng trên, chúng ta sẽ xuống tiền để sử dụng **EFS - Elastic File System** để lưu ảnh. Tạo thêm **ENI - Elastic Network Interface** để giao tiếp giữa **EC2 Instances** và **EFS**. Lưu ảnh vào một mối nên không sợ tinh trạng thất lạc ảnh như bên trên.