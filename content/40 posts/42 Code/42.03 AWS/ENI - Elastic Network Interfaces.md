---
title: "🌱 ENI - Elastic Network Interfaces"
tags: [aws]
date: 2023-03-02
---

## 🌿 What?
-  Là một phần logic của một VPC - Virtual Private Cloud, đại diện cho một **virtual network card**. Cho phép instances kết nối với mạng VPC.
- ENI có thể có những attributes sau:
	- Primary private IP, một hoặc nhiều IPv4 phụ.
	- Một Elastic IP trên tuengf private IPv4
	- Một public IPv4
	- Một hoặc nhiều Security Groups
	- Một địa chỉ MAC
- Khi launch một instance sẽ tự động tạo ra một ENI.
- Có thể tạo một ENI độc lập và sử dụng cho những trường hợp thay thế dự phòng. Ví dụ như Instance1 đang dùng ENI2 mà nó tạch, có thể chuyển ENI2 cho Instance2 để thay thế.
- Bao một AZ chỉ định.
