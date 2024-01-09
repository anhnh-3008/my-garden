---
title: "🌱 Amazon EventBridge"
tags: [aws]
date: 2023-04-08
alias: [eventbridge]
---

## 🌿 What?
- Là dịch vụ hỗ trợ quản lý các sự kiện trigger đến các serivecs của AWS.
- Schedule: Cron jobs
	- vd như mỗi giờ trigger đến [[42 Code/42.03 AWS/AWS Lambda|Lambda]] Function để thực hiện tác vụ gì đó.
- Event Pattern: Event rules xác định tới một service sẽ thực hiện một tác vụ
	- vd: Khi có sự kiện IAM Root User đăng nhập, [[42 Code/42.03 AWS/Amazon SNS - Simple Notification Service|SNS]] sẽ gửi email. 
![[00 Meta/01 Attachments/Pasted image 20230408155728.png]]

## 🌿 Rules
![[00 Meta/01 Attachments/Pasted image 20230408155818.png]]

## 🌿 Schema Registry
- EventBridge có thể phân tích các events trong bus và suy luận được ra **schema**.
- **Schema Registry** cho phép bạn gen code ra cho app, nó sẽ giúp chúng ta biết trước dữ liệu được cấu trúc như thế nào trong bus.
