---
title: "🌱 Amazon ECS - Elastic Container Service"
tags: [aws]
date: 2023-03-26
alias: [ecs]
---

## 🌿 What?
- Là dịch vụ của AWS, giúp dễ dàng chạy và quản lý các [[50 til/51 Code/09 Docker/Docker|Docker]] containers trên 1 cụm EC2 instances hoặc AWS Fargate - một công cụ tính toán không máy chủ cho các containers.
- Launch Docker container on AWS = Launch **EC2 Tasks** trên ECS Cluster.

## 🌿 EC2 Launch Type
- **EC2 Launch Type: bạn phải cung cấp và bảo trì cho cơ sở hạ tầng(là các EC2 instances)**
- Mỗi EC2 Instance phải chạy một ECS Agent để đăng ký trên ECS Cluster. Sau đó, AWS có thể takes care việc starting/stopping các containers.
![[00 Meta/01 Attachments/Pasted image 20230326190905.png]]

## 🌿 Fargate Type
- Launch Docker containers trên AWS mà **không cần tạo bất kỳ một EC2 Instances nào - tất cả đều là serverless**
- Chỉ cần tạo task định nghĩa, AWS sẽ thực hiện chạy ECS Tasks cho chung ta dựa theo lượng CPU/RAM mà chúng ta cần.
- Khi mở rộng, chỉ cần tạo thêm các tasks, không cần tạo thêm EC2 Instances.
- Trong khi đi thi, **Fargate Type được khuyến khích sử dụng hơn vì nó là serverless - dễ mở rộng và quản lý.**
![[00 Meta/01 Attachments/Pasted image 20230326191443.png]]

## 🌿 IAM Roles
- Có 2 dạng ứng với 2 type.
- **EC2 Instance Profile (EC2 Launch Type only):**
	- Chỉ được sử dụng bởi các ECS Agents
	- Tác dụng:
		- Sử dụng để gọi API tới ECS service.
		- Gửi container logs đến CloudWatch Logs
		- Pull Docker image từ ECR
		- Xem các dữ liệu nhạy cảm trong Secrets Manager hoặc SSM Parameter Store.
- **ECS Task Role:**
	- Cho phép các task sử dụng(mỗi task sẽ có những roles được chỉ định)
	- Tác dụng:
		- Sử dụng role để truy cập tới các AWS services của bạn.
		- Task Role được định nghĩa trong **task definition.**
![[00 Meta/01 Attachments/Pasted image 20230326192400.png]]

## 🌿Tích hợp với Load Balancer
- **ALB - Application Load Balancer:** có được hỗ trợ và chạy được với hầu hết các use cases.
- **Network Load Balancer:** nên sử dụng với các use cases cần thông lượng/hiệu suất cao hoặc là khi sử dụng với **AWS Private Link.**
![[00 Meta/01 Attachments/Pasted image 20230326192918.png]]

## 🌿 Data Volumes (EFS)
- Mount thẳng EFS vào ECS tasks.
- Có thể chạy được với cả 2 Type: **EC2 Launch Type and Fargate Type.**
- Các tasks chạy trên bất kỳ AZ nào cũng sẽ chia sẻ chung dữ liệu trên EFS(chung một mối)
- **Fargate + EFS =  Serverless.**
- Use cases: cần chia sẻ và dùng chung dữ liệu cho các containers trên nhiều AZ.
- Note:
	- S3 không thể mount được như một file system.
