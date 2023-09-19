---
title: "🌱 Amazon CloudTrail"
tags: [aws]
date: 2023-04-09
alias: [cloudtrail]
---

## 🌿 What?
- Là dịch vụ cung cấp khả năng ghi lại toàn bộ logs từ các hoạt động của một AWS account.
- Giúp dễ dàng hơn trong việc kiểm tra, tuân thủ của các tài khoản AWS.
- Dịch vụ này được bật mặc định.
- Ghi lại logs từ:
	- Console
	- SDK
	- CLI
	- AWS Services
- Có thể đặt logs của CloudTrail trong [[40123345 posts/42 Code/42.03 AWS/Monitoring/Amazon CloudWatch|CloudWatch]] Logs hoặc [[40123345 posts/42 Code/42.03 AWS/S3|S3]].
- **Một trail có thể áp dụng cho All Regions(mặc định) hoặc chúng ta cũng có thể set cho một region riêng biệt.**
- Nếu một resource bị xóa thì đầu tiên, nó sẽ được ghi vào CloudTrail.

## 🌿 Events
- **Management Events:**
	- Là các events thực hiện trên các resources với AWS account.
	- Ví dụ như:
		- Tạo Security Group
		- Config rules cho routing data(Amazon EC2 CreateSubnet)
	- Mặc định, Trail config là bật để log management events.
	- Có thể tách biệt **Read Event** từ **Write Event**
- **Data Events:**
	- Mặc định cái này không được bật.

## 🌿 Insights
- Bật CloudTrail insight để có thể tìm ra được các hoạt động bất thường trong một AWS account.
- Nó sẽ phân tích các management events bình thường để tạo ra một đường cơ sở, đánh giá được mức độ sử dụng.
- **CloudTrail Insight liên tục phân tích các write events phát hiện sớm các patterns bất thường trong quá trình hoạt động.**
![[00 Meta/01 Attachments/Pasted image 20230409205300.png]]

## 🌿 Retension
- Lưu trong CloudTrail: tối đa 90 ngày
- Trong [[40123345 posts/42 Code/42.03 AWS/S3|S3]]: 4ever.
