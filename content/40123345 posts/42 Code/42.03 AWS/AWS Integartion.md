---
title: "🌱 AWS Integartion"
tags: [aws]
date: 2023-03-25
---

## 🌿 What?
- Trong quá trình phát triển, dự án có thể sử dụng nhiều services lưu trữ và chúng ta cần thực hiện đồng bộ cả về trạng thái cũng như dữ liệu.
- Có 2 parterns để các services giao tiếp với nhau:
	- Đồng bộ trực tiếp giữa 2 services
	- Bất đồng bộ, đặt ở giữa 2 services một Queue, dữ liệu sẽ đi qua queue rồi mới đến service kia.
![[00 Meta/01 Attachments/Pasted image 20230325144616.png]]

- Với cách 1 sẽ có vấn đề là 2 services sẽ có liên kết và bị ảnh hưởng lẫn nhau, nếu một bên bị quá tải thì service còn lại cx sẽ bị ngáo ngơ.
- Vì vậy mà chúng ta cần **tách riêng(decouple)** 2 services. Queue trong AWS có cung cấp 3 services:
	- [[40123345 posts/42 Code/42.03 AWS/Amazon SQS - Simple Queue Service|SQS]]: queue model
	- SNS: pub/sub model
	- Kinesis: real-time streaming model
- Những services này có thể được scale độc lập với app của chúng ta.



