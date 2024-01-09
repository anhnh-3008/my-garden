---
title: "🌱 AWS CloudFront"
tags: [aws]
date: 2023-03-18
---

## 🌿 What?
- Là một dịch vụ CDN(Content Delivery Network)
- **Tăng hiệu suất đọc, content được cache ở edge location.**
	- Ví dụ [[42 Code/42.03 AWS/S3|S3]] đặt ở Singapore, có user truy cập dữ liệu từ Mỹ, dữ liệu sẽ được fetch về một **edge location** ở Mỹ và cache lại, sau đấy, người dùng khác ở Mỹ muốn truy cập dữ liệu thì sẽ đọc ở **edge location** đấy luôn. 
- Nâng cao trải nghiệm của người dùng.
- **DDoS protection(bởi vì là toàn thế giới), tích hợp với Shield, AWS Web Applocation Firewall**

## 🌿 Origins
- **[[42 Code/42.03 AWS/S3|S3]] Bucket**
	- Để phân phối files và caching chúng ở các edge
	- Tăng cường bảo mật với CloudFront **Origin Access Control(OAC)**
	- OAC đang thay thế Origin Access Identity (OAI)
	- CloudFront có thể được sử dụng như một nơi để truy cập để upload files vào S3
- **Custom Origin (HTTP)**
	- Application Load Balancer
	- EC2 Instance
	- S3 website (cần phải bật static web)
	- Bất kỳ HTTP backend nào bạn muốn.

## 🌿 So sánh giữa CloudFront và S3 Replication
- **CloudFront**
	- Global Edge network
	- Files được cached trên các edge location(có thể là một ngày)
	- **Phù hợp cho các static content mà cần available ở mọi nơi**.
- **S3 Cross Region Replication**
	- Cần setup cho từng region mà chúng ta muốn nhân bản.
	- Filed được update gần như là real-time
	- Chỉ được đọc
	- **Phù hợp với những dynamic content cần available với độ trễ thấp ở một vài regions.**

## 🌿 CloudFront Geo Restriction
- Có thể giới hạn người có thể truy cập vào bản phân phối của chúng ta.
	- **Allowlist:** Cho phép người dùng của những khu vực được cho phép, truy cập vào content của bạn
	- **Blocklist:** Ngăn ngừa người dùng của những khu vực chỉ định, không được truy cập vào content của bạn.
- Khu vực sẽ sử dụng một bên thứ 3 - Geo-IP database để giúp chúng ta xác định.
- Use case: Luật bản quyền để kiểm soát truy cập vào dữ liệu.

## 🌿 CloudFront - Pricing
- CloudFront Edge locations ở khắp nơi trên thế giới. Và mỗi khu vực lại có những chi phí khác nhau.
![[00 Meta/01 Attachments/Pasted image 20230321214502.png]]

- Chúng ta có thể giảm số lượng các edge locations để **giảm chi phí**.
- Có 3 price classes:
	1. Price Class All: có trên tất cả các regions - hiệu suất tốt nhất
	2. Price Class 200: hầu hết các regions, trừ những regions có giá thành cao nhất.
	3. Price Class 100: chỉ những regions có chi phí thấp nhất.
![[00 Meta/01 Attachments/Pasted image 20230321215002.png]]
![[00 Meta/01 Attachments/Pasted image 20230321215128.png]]

## 🌿 Cache Invalidations
- Chức năng cho phép xóa dữ liệu trong cache trước khi hết thời gian hết hạn. Tránh tình trạng dữ liệu được cập nhật mới ở S3 những trên các Edge locations vẫn sử dụng phiên bản cũ -> ảnh hưởng đến trải nghiệm của người dùng.
- Chức năng sẽ giúp các edge locations xóa cache để truy cập lại vào orgin để lấy dữ liệu mới nhất.
- Chúng ta có thể refresh toàn bộ(all files - dấu hoa thị) hoặc một phần(/images/hoa thị) cache.