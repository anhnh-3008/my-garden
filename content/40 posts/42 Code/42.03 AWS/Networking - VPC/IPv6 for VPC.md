---
title: "🌱 IPv6 for VPC"
tags: [aws]
date: 2023-04-19
alias: [ipv6]
---

## 🌿 What is IPv6?
- Vì IP v4 chỉ được thiết kế để cung cấp 4.3 tỉ địa chỉ IP, và nó sẽ sớm bị sử dụng hết, chính vì vậy mà IPv6 được ra đời với nhiệm vụ chính để thay thế cho IPv4.
- IPv6 cung cấp **3.4 x 10^38** địa chỉ IP riêng biệt.
- Tất cả các địa chỉ IPv6 đều là public và được định tuyến với internet(không có private range).
- Range được xác định từ 0000 -> ffff, format là x.x.x.x.x.x.x.x.x(x là hexadecimal)
- Ví dụ: 
	- 2001:db6:3333:4444:5555:6666:7777:8888
	- :: -> tất cả 8 phần đều là số 0
	- 2001:db5:: -> 6 phần cuối đều có số 0
	- ::1234:2345 -> 6 phần đầu đều là số 0
	- 2001:db6::1234:2356 -> 4 phần ở giữa đều là số 0

## 🌿 IPv6 in [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]]
- **Lưu ý: Không thể tắt được IPv4 đối với [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]] và subnets**
- Chúng ta có thể bật thêm IPv6 để làm [[40 posts/42 Code/42.03 AWS/Networking - VPC/CIDR, Private and Public IP|public IP]] và sử dụng chung với IPv4.
- Các EC2 Instances sẽ ít nhất phải có 1 public IPv6 và 1 private IPv4.
- [[40 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|Internet Gateway]] có thể tương thích với cả 2 kiểu IP này.
![[00 Meta/01 Attachments/Pasted image 20230419211149.png]]

## 🌿 IPv6 trong Private Subnet
![[00 Meta/01 Attachments/Pasted image 20230419212743.png]]
- Theo luồng của IPv4, cũng có thể áp dụng cho IPv6 khi muốn kết nối internet, chúng ta sẽ tạo một [[40 posts/42 Code/42.03 AWS/Networking - VPC/NAT Gateway|NATGW]] ở Public Subnet để điều hướng requests tới [[40 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|Internet Gateway]], từ đây sẽ gửi requests lên internet.
- Nhưng với IPv6, có thể trực tiếp tạo một Egress-only [[40 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|Internet Gateway]], không cần đi vòng qua 2 thằng trên kia nữa.
- Lưu ý là phải config trên [[40 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|route table]] để kiểm soát traffic đúng yêu cầu sử dụng.
