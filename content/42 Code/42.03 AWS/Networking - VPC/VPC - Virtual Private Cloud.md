---
title: "🌱 VPC - Virtual Private Cloud"
tags: [aws]
date: 2023-04-16
alias: [vpc]
---

## 🌿 What?
- Là dịch vụ cho phép tạo một môi trường mạng ảo trên AWS.
- Giúp chúng ta có thể tạo và quản lý các tài nguyên mạng của mình như route table, subnets, hay tường lửa, ...
- Có thể có nhiều VPCs trong một region.
- Max CIDR trên một VPC là 5 đối với từng CIDR:
	- Min size là /28 - 16 IPs
	- Max size là /16 - 65,536 IPs
- Bởi vì VPC là private IP, nên các giải IP nó nằm trong là:
	- 10.0.0.0/8
	- 172.16.0.0/12
	- 192.168.0.0/16
- VPC CIDR không nên trùng với các mạng khác.

## 🌿 Default VPC
- Tất cả các accounts AWS mới đều có một VPC mặc định.
- Một EC2 Instance sẽ được launch trong VPC mặc định nếu không được chỉ định subnet.
- VPC mặc định có kết nối mạng và tất cả EC2 Instances trong đó sẽ có thể địa chỉ IPv4 public.
- Chúng ta cũng có thể lấy một public và một private IPv4 DNS names.

## 🌿 Subnet VPC
- AWS sẽ giữ lại 5 địa chỉ IP(4 cái đầu tiên và 1 cái cuối cùng) cho từng subnet.
- Chúng ta sẽ không thể assign 5 địa chỉ IP này cho các EC2 Instances được.
- 5 địa chỉ này được giữ lại với mục đích:
	- 10.0.0.0: Network address
	- 10.0.0.1: AWS giữ lại cho VPC router
	- 10.0.0.2: AWS giữ lại để mapping tới DNS
	- 10.0.0.3: AWS giữ lại với mục đích dự phòng, sau này cần thì lôi ra sài.
	- 10.0.0.255: địa chỉ dành cho broadcast, AWS không hỗ trợ cái này nên địa chỉ này vứt xó.
- Nếu trong bài thi có hỏi là cần 29 địa chỉ IP thì có thể suy ra là subnet mask phải cung cấp số địa chỉ IP > 29 + 5 = 34 -> /26 