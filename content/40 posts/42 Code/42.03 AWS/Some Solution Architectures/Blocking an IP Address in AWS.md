---
title: "🌱 Blocking an IP Address in AWS"
tags: [aws]
date: 2023-04-24
alias: []
---

![[00 Meta/01 Attachments/Pasted image 20230424210838.png]]
- Trong thực tế, các dự án không phải là public, việc phải restrict traffic truy cập là việc làm quan trọng, tránh cho hệ thống có tác nhân không được phép sử dụng truy cập ảnh hưởng đến vấn đề bảo mật của hệ thống.
- Có một số cách như:
	- Sử dụng [[40 posts/42 Code/42.03 AWS/Networking - VPC/NACL - Network Access Control List|NACL]]: chặn traffic ở tầng [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]] bằng cách defind ra các deny rules.
	- Security Group của EC2 Instance: defind những traffic nào được phép truy cập vào server.
	- Đặt ALB, chặn trước một EC2 Instance. Nếu sử dụng Network Load Balancer thì phải sài thêm [[40 posts/42 Code/42.03 AWS/Security & Encryption/AWS WAF - Web Application Firewall|WAF]], tường lửa chặn truy cập ở tầng network.
	- Hoặc khi có sử dụng Cloudfront thì cũng cần cài thêm [[40 posts/42 Code/42.03 AWS/Security & Encryption/AWS WAF - Web Application Firewall|WAF]] nếu muốn filter IP addresses mà chúng ta cho phép truy cập vào hệ thống.
