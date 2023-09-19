---
title: "🌱 DMS - Database Migration Service"
tags: [aws]
date: 2023-04-20
alias: [dms]
---

## 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20230420205602.png]]
- Là dịch vụ hỗ trợ migrate database ở bất cứ đâu và đến bất kỳ chỗ nào bạn muốn một cách nhanh chóng và an toàn.
- Có khả năng tự phục hồi cũng như tự động chạy lại nếu có lỗi trong quá trình hoạt động.
- Trong quá trình migrate, main database luôn phải trong trạng thái available.
- Hỗ trợ:
	- Migrate đồng nhất: vd như từ Oracle -> Oracle.
	- Migrate không đồng nhất: vd như Microsoft SQL Server -> [[40123345 posts/42 Code/42.03 AWS/Databases/Amazon Aurora|Aurora]].
- Có thể sử dụng CDC - Continuous Data Relication: thực hiện nhân bản dữ liệu liên tục.
- Sử dụng dịch vụ này, về bản chất chúng ta sẽ phải launch một EC2 Instance, nó sẽ chịu trách nhiệm nhân bản dữ liệu cho chúng ta.
![[00 Meta/01 Attachments/Pasted image 20230420205549.png]]

## 🌿 Schema Conversation Tool(SCT)
- Tính năng hỗ trợ convert schema của database sang engine phù hợp, để bên target có thể migrate được.
![[00 Meta/01 Attachments/Pasted image 20230420210059.png]]

- Best practice:
![[00 Meta/01 Attachments/Pasted image 20230420210320.png]]
- Đặt một server ở on-premise để thực hiện convert schema.
- DMS đặt ở public subnet trên Cloud, thực hiện Migrate + CDC. 