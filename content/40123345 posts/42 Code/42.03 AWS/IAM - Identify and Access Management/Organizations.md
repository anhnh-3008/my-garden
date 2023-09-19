---
title: "🌱 Organizations"
tags: [aws]
date: 2023-04-10
alias: [IAM organizations]
---

## 🌿 What?
- Global service
- Là dịch vụ cho phép quản lý phân cấp trên nhiều AWS accounts. Tăng khả năng quản lý cũng như nhất quán về quyền truy cập và sử dụng tài nguyên của các tài khoản.
- Account chính sẽ là account quản lý, các accounts còn lại là account thành viên.
- Các accounts thành viên chỉ là một phần của organization.
- Thanh toán cho toàn bộ các accounts - thanh toán một lần.
- Nhận được lợi ích về giá từ nhu cầu sử dụng.
- **Chia sẻ reserved instances và saving plans giữa các accounts**.
- Có API để tự động tạo mới một AWS account.

## 🌿 Advantages
- Multi Account vs One account Multi VPC
- Dùng tag tiêu chuẩn để phục vụ mục đính thanh toán.
- Enable CloudTrail cho tất cả các accounts và gửi logs tới S3 của account trung tâm.
- Gửi logs của CloudWatch cho account trung tâm.
- Lập được các Cross Accout Rules với mục đích quản trị.

## 🌿 Security: Service Control Policies(SCP)
- IAM Policies cho phép apply cho OU(Organization Unit) hoặc các accounts để restrict User và Roless.
- Không thể áp dụng đối với account quản lý(management account)
- Cần phải xác định quyền hạn rõ ràng(không cho một account dùng hết các services được).
