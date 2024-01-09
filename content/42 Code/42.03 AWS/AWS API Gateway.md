---
title: "🌱 AWS API Gateway"
tags: [aws]
date: 2023-03-29
alias: [api gateway]
---

## 🌿 What?
- Kết hợp với [[42 Code/42.03 AWS/AWS Lambda|AWS Lambda]]: kiến trúc không có server.
- Expose REST API.
- Hỗ trợ giao thức WebSocket
- Xử lý API versioning(v1,v2,...)
- Xử lý giữa các môi trường phát triển khác nhau(dev, test, prod, ...)
- Xử lý bảo mật(Authen & Authori)
- Tạo API keys
- Kết hợp được với Swagger/Open API để nhanh chóng tạo ra doc.
- Có thể transform và validate requests và responses.
- Gen ra SDK và API specifications.
- Cache lại responses của API.

## 🌿 Integrations
Kết hợp được với:
- **[[42 Code/42.03 AWS/AWS Lambda|Lambda]] Function**
- **HTTP**
	- Dùng để add rate limit, caching hoặc authen cho users, ...
- **AWS Service**

## 🌿 Endpoint Types
- **Edge-Optimized(default)**
	- Cho global clients
	- Requests sẽ được định tuyến tới các edge location(độ trễ thấp)
	- API Gateway chỉ tồn tại trên một region nhưng users ở những chỗ khác vẫn truy cập với độ trễ thấp.
- **Region**
	- Cho những clients ở cùng một region
	- Có thể kết hợp thủ công với CloudFront
- **Private**
	- Chỉ có thể kết nối từ VPC thông qua ENI.
	- Sử dụng policy để xác định quyền truy cập.

## 🌿 Security
- **Dùng để xác thực người dùng**:
	- IAM roles(phù hợp với các app nội bộ)
	- Cognito (xác định các user bên ngoài - vd như mobiles user)
	- Custom Authorizer (cho logic của chúng ta)
- **Custom Domain Name HTTPS** bằng việc tích hợp AWS Certificate Manager(ACM)
	- Nếu sử dụng Edge-Optimized endpoint, certificate phải thuộc về **us-east-1**
	- Nếu sử dụng Regional endpoint, certificate phải nằm trong API Gateway region
	- Nếu dùng với Route53, phải sử dụng CNAME hoặc A-alias.
