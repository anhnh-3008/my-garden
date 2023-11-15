---
title: "🌱 SSM Parameter Store"
tags: [aws]
date: 2023-04-15
alias: [parameter store]
---

## 🌿 What?
- Là dịch vụ lưu trữ các thông tin câu hình, khóa bí mật. Bảo mật thông qua IAM.
- Có thể sử dụng [[40 posts/42 Code/42.03 AWS/Security & Encryption/AWS KMS - Key Management Service|KMS]] để mã hóa dữ liệu.
- [[40 posts/42 Code/42.03 AWS/Some Solution Architectures/Serverless|Serverless]], có khả năng mở rộng, bền bỉ và sử dụng dễ dàng với SDK.
- Quản lý version của các thông tin như cấu hình hay khóa bí mật.
- Gửi thông báo tới AWS [[40 posts/42 Code/42.03 AWS/Monitoring/Amazon EventBridge|EventBridge]].
- Tích hợp với CloudFormation.
![[00 Meta/01 Attachments/Pasted image 20230415111940.png]]

## 🌿 Hierarchy
![[00 Meta/01 Attachments/Pasted image 20230415112058.png]]

## 🌿 Tier
| |Standard|Advance|
|------|---------|---------|
|tổng số param lưu trữ(cho 1 account/region) | 10,000| 100,000|
|size tối đa của 1 param | 4Kb | 8Kb |
|param policy available | No | Yes |
| Chi phí | không cần cọc | phải cọc |
| Chi phí lưu trữ | miễn phí | 0.05$ cho mỗi param/ tháng|

## 🌿 Parameters Policy
- Có thể assign TTL để thực hiện update hoặc xóa các thông tin nhạy cảm ví dụ như mật khẩu chẳng hạn.
- Có thể assign một lúc nhiều policies.
![[00 Meta/01 Attachments/Pasted image 20230415112851.png]]