---
title: "🌱 AWS Global infrastructure"
tags: [aws]
date: 2023-02-21
---

## AWS Cloud Use Cases
- 🌱 Enterprise IT(chuyển giao công nghệ), Backup & Storage, Big Data analytics 
- 🌱 Website hosting, Mobile & Social Apps
- 🌱 Gaming, ...

## Global infrastructure
- 🌱 Regions
- 🌱 Availability Zones(AZs)
- 🌱 Data Centers
- 🌱 Edge Locations / Points of Presence

### Regions
- 🌱 Là khu vực vật lý, một cụm nhiều AZs, tối thiểu là 3, không quá 6.
- 🌱 Tên: eu-west-3, eu-east-1, ...

> [!question] How to choose an AWS region?
> 
> Some factors could be impact to your choice:
> 
> 	1.  Compliance with data governance and legal requirements: xem xét dự án có dữ liệu chỉ được lưu hành trong nước không(ví dụ như dự án phục vụ chính phủ) -> chọn region phù hợp.
> 
> 	2.  Proximity to customers: Xem xét tập khách hàng chủ yếu truy cập từ đâu -> chọn region gần đó sẽ giảm thiểu được độ trễ.
> 
> 	3. Available Services within a Region: Không phải tất cả các Regions đều có đầy đủ Services. Xác định rõ services sẽ được sử dụng để lựa chọn Region phù hợp. Xem các available services cho từng khu vực ở [đây 👇](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).
> 
> 	4. Pricing: Mỗi region có một giá khác nhau, đây cũng là một yếu tố cần cân nhắc khi chọn AWS region.

### Availability Zones(AZs)
- 🌱 Cách nhau tối thiểu 100km, độc lập, tránh các TH thiên tai.
- 🌱 Là tập hợp của một hoặc nhiều trung tâm dữ liệu riêng biệt, bao gồm:
	- Nguồn điện dự phòng.
	- Networking.
	- Được liên kết với một AWS Region.
- 🌱 Tất cả AZs trong một AWS Region đều được kết nối với nhau với điều kiện:
	- Băng thông cao
	- Độ trễ cực thấp
	- Networking

### Edge Locations
- 🌱 Chứa CloudFront(Amazon's content delivery network - CDN): truyền tải dữ liệu đến end-user với độ trễ thấp nhất có thể.

### AWS Service liên quan đến AWS Solution Architect Exam

![[00 Meta/01 Attachments/Screenshot 2023-02-22 at 13.42.03.png]]

And more ...