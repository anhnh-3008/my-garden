---
title: "🌱 Transit Gateway"
tags: [aws]
date: 2023-04-18
alias: [transit gateway]
---

## 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20230418215533.png]]
- Với rất nhiều các dịch vụ sử dụng để kết nối giữa các VPCs, từ VPCs kết nối tới on-premise, các VPCs ở khác regions, ... Chính vì thế sẽ rất dễ làm cho cấu trúc liên kết mạng của hệ thống bị phức tạp, lâu dần sẽ khó mở rộng hoặc bảo trì, chưa kế đến vấn đề chi phí.
- Giải pháp là sử dụng Transit Gateway, như kiểu cafe 3in1, có sữa có đường có cafe, chỉ cần đổ nước nóng vào là uống thôi.
![[00 Meta/01 Attachments/Pasted image 20230418215840.png]]
- Có thể kết nối giữa các region.
- Chia sẻ trên nhiều accounts, sử dụng Resource Access Manager(RAM)
- Có thể sử dụng peer Transit Gateway trên nhiều region.
- Khi kết nối nhiều VPCs về một mối, cần chú ý setup [[42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|route table]] để kiểm soát traffic giữa các VPCs, tránh không cho giao tiếp lung tung.
- Hỗ trợ **IP Multicast**

## 🌿 ECMP - Equal-Cost Multi-Part routing
![[00 Meta/01 Attachments/Pasted image 20230418220403.png]]
- Sử dụng ECMP để giải quyết khi gặp bài toán cần kết nối với nhiều VPCs.


## 🌿 Share Direct Connection between multiple accounts
![[00 Meta/01 Attachments/Pasted image 20230418220706.png]]
- Tạo cái Direct Connection Gateway(ko share cho nhiều accounts được) ở ngoài, trỏ tới Transit Gateway để nó share cho các VPCs ở những accounts khác.