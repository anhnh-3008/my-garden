---
title: "🌱 AWS Site-to-Site VPC"
tags: [aws]
date: 2023-04-18
alias: [site-to-site, s2s]
---

## 🌿 What?
- Là kiến trúc giúp kết nối các resources trong Private Subnet tới các server on-premise.
![[00 Meta/01 Attachments/Pasted image 20230418211559.png]]
- Gồm 3 thành phần:
	- Virtual Private Gateway đặt ở VPC trên AWS, có tránh nhiệm là cổng kết nối bên Cloud.
	- Cổng kết nối bên on-premise là Custimer Gateway(public IP) hoặc là NAT Device.
- **Lưu ý:**  Phải nhớ bật **Route Propagation** để kết nối Virtual Private Gateway với VPC.
- VPN CloudHub: Sử dụng khi cần kết nối đến nhiều servers on-premise.
