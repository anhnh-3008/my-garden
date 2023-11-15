---
title: "🌱 VPC Peering"
tags: [aws]
date: 2023-04-17
alias: [vpc peering]
---

## 🌿 What?
- Là dịch vụ để tạo một kết nối riêng tư giữa 2 [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]] sử dụng network của AWS.
- Nó giúp cho các resources của 2 [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]] như cùng chung một network.
- Để sử dụng dịch vụ này, phải chắc chắn rằng không được overlap CIDRs.
- Không có tính chất bắc cầu.
![[00 Meta/01 Attachments/Pasted image 20230417222859.png]]
- Nhớ là phải update [[40 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|route table]] để chúng có thể giao tiếp được với nhau.

- Có thể tạo VPC Peering giữa các VPCs ở khác accounts hoặc regions.
- Có thể reference security group trong một peered VPC. 

