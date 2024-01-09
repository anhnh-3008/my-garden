---
title: "🌱 Micro Services Architecture"
tags: [aws, architecture]
date: 2023-04-04
---

## 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20230404195416.png]]
- Bạn có thể tự do thiết kế từng micro-service theo cách bạn muốn.
- Patterns đồng bộ: API Gateway, Load Balancers.
- Patterns bất đồng bộ: SQS, Kinesis, SNS, Lambda triggers (S3)
- Thách thức với micro-services:
	- Chi phí
	- Tối ưu
	- Phức tạp khi phải quản lý nhiều versions của nhiều services.
	- Yêu cầu code nhiều hơn để tích hợp với nhiều services.
- Một số thách thức được giải quyết với kiến trúc serverless.
	- API Gateway, Lambda tự động scale và chúng ta phải trả theo nhu cầu sử dụng.
	- Có thể dễ dàng clone API, Dùng lại được các môi trường.

