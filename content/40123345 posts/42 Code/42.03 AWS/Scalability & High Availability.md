---
title: "🌱 Scalability & High Availability"
tags: [aws]
date: 2023-03-05
---

## 🌿 Scalability
- Khả năng mở rộng linh hoạt dự theo yêu cầu của khách hàng. Hệ thống có khả năng thích nghi tốt với trạng thái của ứng dụng.
- Scalability có liên quan đến High Availability.
- Có 2 loại scalability:
	- Vertical scalability
	- Horizontal scalabilily

### 🍃 Vertical scalability
![[00 Meta/01 Attachments/Pasted image 20230305175947.png]]
- Mở rộng về phần cứng của instance để xử lý các yêu cầu nhanh và chính xác hơn.
- Vd t2.micro -> t2.large
- Vertical scalability rất thường được sử dụng với những hệ thống không phân tán, ví dụ như database.
- RDS, ElasticCache là những services có thể sử dụng để thực hiện scale vertically.
- Thường có giới hạn về khả năng scale vertically(hardware limit)

### 🍃 Horizontal scalability
![[00 Meta/01 Attachments/Pasted image 20230305180205.png]]
- Mở rộng về số lượng instances, số lượng hệ thống của ứng dụng để có thể đáp ứng được nhiều yêu cầu của người dùng hơn.
- Dành cho những hệ thống phân tán.
- Thường được xử dụng cho web applications / modern applications.
- Dễ dàng để scale horizontally với EC2 service.

## 🌿 High Availability
- High Availability thường sẽ được hiểu như scale horizontally.
- HA là ứng dụng của chúng ta được chạy trên ít nhất 2 data centers(AZs) mục đích để hệ thống luôn sẵn sàng sử dụng ngay cả khi có sự cố ở một data center nào đó.
