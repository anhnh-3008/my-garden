---
title: "🌱 Placement Groups"
tags: [aws]
date: 2023-03-01
---

## 🌿 What?
- 🌱 Về cơ bản, placement group cho phép chúng ta quản lý vị trí - nơi khởi chạy các EC2 Instances, từ đó nâng cao hiệu suất, giảm độ trễ , ...
- 🌱 Có 3 strategies: Cluster, Spread, Partition

### 🌿 Cluster
![[00 Meta/01 Attachments/Pasted image 20230301224923.png]]
- Các EC2 Instances cùng nằm trong một hardware - same rack, same AZ.
- Ưu: 
	- Great network - độ trễ rất thấp, 10Gbps network.
- Nhược:
	- Chết là chết tất. Rủi ro cao.
- Use cases:
	- Những dự án yêu cầu độ trễ cực thấp và khả năng truyền tải dữ liệu nhanh.

### 🌿 Spread
![[00 Meta/01 Attachments/Pasted image 20230301225129.png|500]]
- Các EC2 Instances không cùng một một chỗ, thay vào đó sẽ được đặt riêng ở các hardwares khác nhau, ở nhiều AZ trên cùng một Region. 
- Ưu:
	- Giảm rủi ro chết chùm.
- Nhược:
	- Giới hạn 7 instances cho mỗi placement group trên cùng một AZ(nhược với những dự án big size).
- Use cases:
	- Những dự án đề cao khả năng availability(app mạng xã hội, ...)
	- Những dự án quan trọng, cần đảm bảo ít rủi ro.

### 🌿 Partition
![[00 Meta/01 Attachments/Pasted image 20230301225752.png|500]]
- Kết hợp giữa Cluster và Spread. Mỗi một AZ có thể chứa 7 partions, mỗi một partion chứa những EC2 Instances - same rack.
- Ưu:
	- Đảm bảo độ trễ cực thấp + truyền tải dữ liệu cao giữa các instances.
	- Giảm thiểu rủi ro khi một partion chết, các partions khác vẫn hoạt động bình thường.
	- Có thể setup hàng trăm EC2 Instances, xịn hơn spread nhiều.
- Có thể xem thông tin vị trí của instance thông qua metadata của instance.
- Use cases: 
	- Khi chúng ta có dự án có thể nhận biết phân vùng để truyền tải dữ liệu, các ứng dụng big data sử dụng: HDFS, HBase, Cassandra án Apache Kafka