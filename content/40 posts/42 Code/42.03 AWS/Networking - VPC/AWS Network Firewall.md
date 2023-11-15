---
title: "🌱 AWS Network Firewall"
tags: [aws]
date: 2023-04-19
alias: [network firewall]
---

## 🌿 What?
- Bảo vệ cho toàn bộ [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]].
- Bảo vệ từ Layer 3 và 7.
- Nó sử dụng AWS Network Load Balancer
- Các rules được define được quản lý toàn bộ trên [[40 posts/42 Code/42.03 AWS/Security & Encryption/AWS Firewall Manager|AWS Firewall Manager]], để có thể áp dụng cho nhiều VPCs của nhiều accounts.
![[00 Meta/01 Attachments/Pasted image 20230419220255.png]]

- Hỗ trợ có thể define tới 1000 rules.
- Traffic Filtering: Allow, drop hoặc aleart nếu bắt gặp traffic match với các rules đã define.
- Active Flow Inspection: một biện pháp bảo vệ. Ngăn chặn các truy cập bất thường(giống như Network Load Balancerr)
- Có thể send log tới S3, Athena, ... kết hợp với các dịch vụ khác để lưu trữ hoặc phân tích tùy theo nhu cầu của hệ thống.
