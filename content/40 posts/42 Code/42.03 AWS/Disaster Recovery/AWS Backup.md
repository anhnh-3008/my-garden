---
title: "🌱 AWS Backup"
tags: [aws]
date: 2023-04-20
alias: [aws backup]
---

## 🌿 What?
- Là dịch vụ được quản lý hoàn toàn bởi AWS.
- Hỗ trợ chúng ta quản lý cũng như tự động backups cho nhiều AWS Services.
- Không cần phải tạo custom script hay những tiến trình thủ công, AWS lo tất.
- Các services được hỗ trợ:
	- EC2 / [[40 posts/42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]]
	- [[40 posts/42 Code/42.03 AWS/S3|S3]]
	- [[40 posts/42 Code/42.03 AWS/Databases/Amazon RDS - Relational Database Service|RDS]] / [[40 posts/42 Code/42.03 AWS/Databases/Amazon Aurora|Aurora]] / [[40 posts/42 Code/42.03 AWS/Databases/Amazon DynamoDB|DynamoDB]]
	- DocumentDB / Neptune
	- EFS / FSx
	- Storage Gateway
- Hỗ trợ backup trên nhiều regions và accounts.
- **Backup Plans** - có thể hiểu là Backup policies:
	- Tần suất backup - 1h, daily, weekly, ...
	- Backup windows
	- Transaction to Cold Storage(never, 1 day, month, ...)
	- Chu kỳ giữ lại(always, day, weeek, ...)
![[00 Meta/01 Attachments/Pasted image 20230420213933.png]]

## 🌿 Backup Vault Lock
- Chỉ có ghi vào và đọc chứ không có xóa được.