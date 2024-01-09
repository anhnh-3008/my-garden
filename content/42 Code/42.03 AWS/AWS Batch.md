---
title: "🌱 AWS Batch"
tags: [aws]
date: 2023-04-27
alias: [batch]
---

## 🌿 What?
- Do AWS quản lý hoàn toàn.
- Hỗ trợ chạy các tác vụ theo lô(kiểu như xử lý ảnh khi người dùng gửi lên [[42 Code/42.03 AWS/Elastic Beanstalk|S3]], ...)
- Batch sẽ linh động tạo ra các EC2 Instances hoặc Spot Instances để xử lý logic, nó sẽ tự biết lựa chọn về compute/memory phù hợp.
- Các Batch jobs được định nghĩa như là các [[50 til/51 Code/09 Docker/Docker|Docker]] Imaged và sẽ chạy trên [[42 Code/42.03 AWS/Databases/Amazon ECS - Elastic Container Service|ECS]].
- Phù hợp khi chúng ta muốn tối ưu chi phí cũng như đơn giản hoá kiến trúc của hệ thống.
![[00 Meta/01 Attachments/Pasted image 20230427162102.png]]

|AWS Lambda|AWS Batch|
|--------------|----------|
|Time limit| No time limit|
|Limit runtime|Cứ chạy cái docker là sử dụng tẹt ga|
|Giới hạn bộ nhớ tạm| Phụ thuộc vào EBS/instance store|
|Serverless| Có launch EC2 Instance(được AWS quản lý)|
