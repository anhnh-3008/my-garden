---
title: "🌱 CIDR, Private and Public IP"
tags: [aws]
date: 2023-04-16
alias: [CIDR, private IP, public IP]
---

## 🌿 CIDR - Classless Inter-Domain Routing
- Là một method thực hiện viêc phân bổ các địa chỉ IP.
- Được sử dụng trong **Security Groups** và networking của AWS nói chung.
![[00 Meta/01 Attachments/Pasted image 20230416100447.png]]
- Giúp chúng ta define một dải địa chỉ IP:
	- WWW.XX.YY.ZZ/34 => một IP
	- WWW.XX.YY.ZZ/0 => tất cả IPs trong dải đó.
	- Nhưng chúng ta có thể define: 192.168.0.0/26 => đại diện cho một dải 64 IPs 192.168.0.0 -> 192.168.0.63

## 🌿 Ingredients
- Gồm 2 phần:
	- **Base IP**
		- Đại diện cho một dải IP.
		- 10.0.0.0, 192.168.0.0, ...
	- **Subnet Mask**
		- Xác định số lượng bits có thể thay đổi được trên IP
		- Các dạng hay gặp:
			- 8 <=> 255.0.0.0
			- 16 <=> 255.255.0.0
			- 24 <=> 255.255.255.0
			- 32 <=> 255.255.255.255

- Cách xác định dải IP từ Subnet Mask:
![[00 Meta/01 Attachments/Pasted image 20230416102226.png]]

192.168.0.0/24 2^(32-24) IP <=> 192.168.0.0 -> 192.168.0.255

## 🌿 Private & Public IP
- **Private IP là các dải sau:**
	- 10.0.0.0 -> 10.255.255.255 (10.0.0.0/8)
	- 172.16.0.0 -> 172.31.255.255 (172.16.0.0/12) -> dải địa chỉ IP của AWS VPC
	- 192.168.0.0 -> 192.168.255.225 (192.168.0.0/16)
- **Tất cả các IPs còn lại thì là Public IP.**