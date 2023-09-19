---
title: "🌱 VPC Endpoint"
tags: [aws]
date: 2023-04-18
alias: [vpc endpoint]
---

## 🌿 What?
- Là dịch vụ giúp chúng ta có thể kết nối trực tiếp từ trong private subnet tới các services khác của AWS, thông qua một private network của AWS được gọi là **privatelink**, thay vì thông qua internet.
- Có thể đáp ứng tốt theo nhu cầu sử dụng, nó scale theo chiều ngang.
- Không cần phải setup thêm [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|IGW]], [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/NAT Gateway|NATGW]], ... để kết nối. Giảm thiểu chi phí sử dụng.
- Khi có vấn đề, lưu ý các thông tin sau:
	- Kiểm tra lại DNS Setting Solution trong [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]].
	- Kiểm tra lại [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|Route Table]] xem đã định tuyến đúng chưa.
![[00 Meta/01 Attachments/Pasted image 20230418204559.png]]

## 🌿 Types
- **Interface Endpoints (sử dụng privatelink)**
	- Cung cấp một ENI như một entrypoint, và nó phải được gán security group để kiểm soát traffic.
	- Hỗ trợ cho hầu hết các services của AWS.
	- Thanh toán theo giờ + GB dữ liệu xử lý.
- **Gateway Endpoints**
	- Cung cấp một gateway và sử dụng route table để kiểm soát traffic, không dùng security group như thằng bên trên.
	- Hỗ trợ cho S3 và DynamoDB.
	- Miễn phí
![[00 Meta/01 Attachments/Pasted image 20230418205018.png]]

- **Với S3 nên sử dụng Gateway hay Interface endpoints?**
	- Thông thường trong hầu hết các trường hợp, gateway luôn được ưu tiên sử dụng do nó miễn phí.
	- Chỉ khi chúng ta cần kết nối S3 với server on-premise, từ một VPC hoặc region khác, thì cần phải sử dụng với Interface Endpoints.
