---
title: "🌱 NAT Instance"
tags: [aws]
date: 2023-04-17
alias: [nat instance]
---

## 🌿 What?
- NAT - Network Address Translation
- Là một EC2 Instance trung gian giúp các EC2 Instances trong private subnets có thể kết nối được với internet.
- NAT Instance phải được launch public
- Phải tắt setting trong EC2: **Source / destination check**
- Phải attach ElasticIP cho NAT Instance.
- Phải config thêm [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|Route Table]] để định tuyến traffic của các EC2 Instance trong Private Submet sang NAT Instance.
![[00 Meta/01 Attachments/Pasted image 20230417211518.png]]

- Kiến trúc tương tự như sử dụng [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|IGW]], những sẽ thay thế bằng NAT Instance.
![[00 Meta/01 Attachments/Pasted image 20230417211707.png]]

## 🌿 Notes
- Không được hỗ trợ kể từ 31/12/2020
- Không HA/ không tự động thiết lập lại nếu có lỗi.
	- Cần phải config thêm như sử dụng [[40123345 posts/42 Code/42.03 AWS/ASG - Auto Scaling Group|ASG]] + script để resilient setup.
- Băng thông kết nối internet phụ thuộc vào EC2 Instance Type
- Ngoài ra chúng ta còn cần phải quản lý thêm Security Groups và Roles của Instance.
- Nên lựa chọn sử dụng [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/NAT Gateway|NAT Gateway]] thay vì NAT Instance, nó outdate rồi.
