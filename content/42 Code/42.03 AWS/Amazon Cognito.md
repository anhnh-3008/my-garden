---
title: "🌱 Amazon Cognito"
tags: [aws]
date: 2023-03-31
alias: [cognito]
---

## 🌿 What?
- Là dịch vụ cấp phát cho người dùng định danh để có thể giao tiếp với các web hoặc mobile apps.
- **Cognito User Pools:**
	- Đăng nhập cho người dùng app.
	- Tích hợp được với [[42 Code/42.03 AWS/AWS API Gateway|API Gateway]] & Application Load Balancer.
- **Cognito Identity Pools:**
	- Cung cấp AWS credentials để user có thể truy cập trực tiếp vào các AWS Services.
	- Tích hợp với Cognito User Pools như một nơi cung cấp định danh.
- **Cognito vs IAM:** 
	- Hàng trăm users.
	- Sử dụng cho cả mobile users.
	- Xác thực với SAML.
## 🌿 Cognito User Pools(CUP)
- Tính năng:
	- Tạo ra một database không máy chủ lưu dữ liệu người dùng cho web hoặc mobile apps.
	- Simple login
	- Password reset
	- Verify email/phone number
	- MFA
	- Login với bên thứ3 - Facebook, Github, SAML, ...

- Mô hình tích hợp với [[42 Code/42.03 AWS/AWS API Gateway|API Gateway]] và ALB:
![[00 Meta/01 Attachments/Pasted image 20230331150227.png]]


## 🌿 Cognito Identity Pools
- Diagram:
![[00 Meta/01 Attachments/Screenshot 2023-03-31 at 15.08.15.png]]

## 🌿 Row level Security in DynamoDB
- Có thể thông qua Cognito để chỉ định user được đọc những row nào trong [[40123345 posts/42 Code/42.03 AWS/Amazon DynamoDB|DynamoDB]].
![[00 Meta/01 Attachments/Pasted image 20230331151223.png]]