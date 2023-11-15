---
title: "🌱 Serverless"
tags: [aws, architecture]
date: 2023-03-27
alias: [serverless]
---

## 🌿 What?
- Là một mô hình mới, các developers không cần phải quản lý bất kỳ một cái server nào.
- Chúng chỉ để deploy code, functions.
- FaaS = Function as a Service
- Serverless được triển khai đầu tiên với AWS Lambda những hiện tại mô hình này đã có thể kết hợp với bất kể cái gì có thể quản lý được: databases, messaging, storage, ...
- **Serverless không phải là hoàn toàn không có servers nào**, nó chỉ có nghĩa là chúng ta không cần quản lý, cung cấp hay nhìn thấy các servers thôi.

## 🌿Mô hình serverless trong AWS
- Trong AWS, các services hỗ trợ chúng ta build một mô hình serverless bao gồm:
	- AWS Lambda
	- DynamoDB
	- AWS Cognito
	- AWS API Gateway
	- Amazon [[40 posts/42 Code/42.03 AWS/S3|S3]]
	- AWS [[40 posts/42 Code/42.03 AWS/Amazon SNS - Simple Notification Service|SNS]] & [[40 posts/42 Code/42.03 AWS/Amazon SQS - Simple Queue Service|SQS]]
	- AWS Kinesis Data Firehose
	- Aurora Serverless
	- Step Functions
	- Fargate
![[00 Meta/01 Attachments/Pasted image 20230327214338.png]]

