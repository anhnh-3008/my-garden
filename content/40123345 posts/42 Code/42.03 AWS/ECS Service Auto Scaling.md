---
title: "🌱 ECS Service Auto Scaling"
tags: [aws]
date: 2023-03-27
---

## 🌿 What?
- Tự động tăng hoặc giảm số lượng desired(mong muốn) của ECS tasks.
- Sử dụng **AWS Application Auto Scaling**
	- Scale theo CPU
	- Theo RAM
	- Theo số lượng request đếm được ở ALB
- **Target Tracking** - scale dựa theo giá trị của một thông số chỉ định CloudWatch.
- **Step Scaling** - scale dựa theo CloudWatch Alarm chỉ định.
- **Scheduled Scaling** - scale dựa theo thời gian chỉ định(có thể dự đoán được thay đổi)

- ECS Service Auto Scaling là ở **tasks level** != EC2 Auto Scaling là ở **EC2 instance level**.
- Fargate Auto Scaling dễ dàng setup hơn vì nó là **serverless**.

## 🌿 Auto Scaling EC2 Instances
- Là Add thêm EC2 Instances.
- **Auto Scaling Group Scaling**
	- Scale ASG dựa theo CPU
	- Add thêm EC2 Instances để đáp ứng nhu cầu sử dụng thực tế.
- **ECS Cluster Capacity Provider**
	- Tự động cung cấp cũng như mở rộng cơ sở hạ tầng cho các ECS Tasks của chúng ta.
	- Capacity Provider được kết hợp với một Auto Scaling Group.
	- Add EC2 Instances khi thiếu capacity(CPU, RAM, ...)

- Luôn ưu tiên sử dụng **ECS Cluster Capacity Provider**.

