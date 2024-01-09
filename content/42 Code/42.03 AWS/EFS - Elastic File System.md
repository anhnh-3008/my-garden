---
title: "🌱 EFS - Elastic File System"
tags: [aws]
date: 2023-03-04
---

## 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20230304223657.png]]
- Hệ thống quản lý file, có thể mounted tới nhiều EC2 Instances, ở nhiều AZ khác nhau. Một giải pháp hiệu quả để chia sẻ các files trên môi trường cloud.
- Highly available, dễ dàng scale, chi phí(gấp 3 lần gp2), dùng đến đâu trả tiền đến đấy.
- Use case: content management, web serving, data sharing, wordpress
- Sử dụng giao thức NFSv4.1
- Sử dụng Security Group để kiểm soát truy cập tới EFS.
- Tương thích với Linux based AMI(not Windows)
- Mã hóa sử dụng KMS
- Scale tự động, dùng đến đâu trả đến đấy, không có đặt trước hay gì cả.


