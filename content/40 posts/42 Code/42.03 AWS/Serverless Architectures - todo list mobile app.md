---
title: "🌱 Serverless Architectures - Todo list mobile app"
tags: [aws]
date: 2023-03-31
---

## 🌿 Requirements
- Tạo một mobile app:
	- Expose REST API với HTTPS
	- Kiến trúc [[40123345 posts/42 Code/42.03 AWS/Serverless|serverless]].
	- User có thể tương tác trực tiếp với folder của họ trên [[40 posts/42 Code/42.03 AWS/S3|S3]]
	- User cần xác thực thông qua một service quản lý không máy chủ.
	- User có thể đọc và ghi mới các to-do, nhưng thường chủ yếu là họ sẽ đọc.
	- Database có thể scale và có thông lượng có khả năng đọc cao.

## 🌿 Serverless Architecture 
![[00 Meta/01 Attachments/Pasted image 20230331160701.png]]

- Sử dụng [[40 posts/42 Code/42.03 AWS/AWS API Gateway|API Gateway]] để expose các HTTP API và để gọi đến các [[40 posts/42 Code/42.03 AWS/AWS Lambda|Lambda]] function.
- [[40 posts/42 Code/42.03 AWS/AWS Lambda|Lambda]] function dùng để xử lý logic và query vào database
- Database sử dụng [[40123345 posts/42 Code/42.03 AWS/Amazon DynamoDB|DynamoDB]] để đáp ứng kiến trúc không máy chủ.
- Về vụ xác thực sử dụng [[40 posts/42 Code/42.03 AWS/Amazon Cognito|Amazon Cognito]] để định danh cho người dùng. Sử dụng [[40 posts/42 Code/42.03 AWS/Amazon Cognito|Cognito]] Indentity pool để cung cấp certificate cho người dùng. Người dùng có thể sử dụng nó để thực hiện các tác vụ với [[40 posts/42 Code/42.03 AWS/S3|S3]].
- Để nâng cao khả năng đọc dữ liệu từ trong DB, sử dụng DAX làm lớp layer giữa [[40 posts/42 Code/42.03 AWS/AWS Lambda|Lambda]] và [[40123345 posts/42 Code/42.03 AWS/Amazon DynamoDB|DynamoDB]]. Giúp cache lại các thông tin hay được sử dụng, từ đó nâng cao hiệu suất đọc cũng như giảm thiểu các câu queries tới [[40123345 posts/42 Code/42.03 AWS/Amazon DynamoDB|DynamoDB]].
