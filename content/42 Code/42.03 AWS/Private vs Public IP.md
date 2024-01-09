---
title: "🌱 Private vs Public IP"
tags: [aws]
date: 2023-03-01
---

## 🌿 Overview
- 🌱 Có 2 loại IP:
	- IPv4: [0-255].[0-255].[0-255].[0-255], ex: 1.160.10.250
	- IPv6
- 🌱 IPv4 vẫn là format phổ biến nhất dùng cho web
- 🌱 IPv6 mới hơn và được sử dụng cho IoT.
- 🌱 IPv4 cho phép 3.7 tỷ địa chỉ khác nhau được public trên mạng/

## 🌿 So sánh Private và Public IP
- 🌱 Public IP:
	- Để máy chủ có thể định danh trên internet.
	- Uniq, không trùng với bố con thằng nào trên internet.
	- Có thể định vị vị trí thông qua public IP.
	- Thay đổi khi reboot lại instace.
- 🌱 Private IP:
	- Để định danh máy trong một mạng nội bộ.
	- Phải Uniq trong mạng nội bộ.
	- 2 Companies khác nhau có thể có cùng một IP.
	- Những máy trong mạng nội bộ sẽ kết nối với WWW thông qua một internet gateway(a proxy)
	- Chỉ một range của IP được chỉ định mới có thể sử dụng như private IP.
	- Không thay đổi khi reboot lại instace.

## 🌿 Elastic IP
- 🌱 Như IP bình thường, khác cái là nó độc lập với instance, vì vậy chúng ta có thể dễ dàng thay đổi instance mà không cần gán lại địa chỉ IP.
- 🌱 Chỉ có thể có 5 Elastic IP trong 1 tài khoản(có thể yêu cầu tăng thêm)
- 🌱 Nên tránh dùng:
	- Chi phí
	- Quản lý
	- Khả năng mở rộng