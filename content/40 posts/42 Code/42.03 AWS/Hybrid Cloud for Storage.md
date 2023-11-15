---
title: "🌱 Hybrid Cloud for Storage"
tags: [aws]
date: 2023-03-23
---

## 🌿 What?
- AWS thúc đẩy hybrid cloud
	- Một phần thuộc về cơ sở hạ tầng trên cloud
	- Một phần thuộc về cơ sở hạ tầng(mặt đất) của chúng ta.
- Vậy làm thế nào để chúng ta có thể cho dữ liệu được giao tiếp mượt mà giữa hai hạ tầng đó? - **AWS Storage Gateway**

## 🌿 AWS Storage Cloud Native Options
![[00 Meta/01 Attachments/Pasted image 20230323222856.png]]

## 🌿 AWS Storage Gateway
- Là cầu nối giữa dữ liệu 'mặt đất' và dữ liệu trên cloud
![[00 Meta/01 Attachments/Pasted image 20230323223125.png]]
- **Use cases:**
	- Phục hồi thảm họa
	- Backup & restore
	- Làm tầng lưu trữ
	- cache
- Types:
	- **S3 File Gateway**
	- **FSx File Gateway**
	- **Volume Gateway**
	- **Tape Gateway**

### 🍃 S3 File Gateway
![[00 Meta/01 Attachments/Pasted image 20230323223809.png]]
- Có thể truy cập S3 File Gateway thông qua 2 giao thức là NFS và SMB.
- **Hầu hết các dữ liệu thường xuyên được truy cập sẽ năm ở file gateway.**
- Hỗ trợ S3 Standard, S3 Standard IA, S3 One Zone A, S3 Intelligent Tiering.
- **Chuyển dữ liệu tới S3 Glacier bằng Lifecrycle Policy.**
- Bucket sử dụng IAM roles để truy cập cho từng File Gateway.
- Giao thức SMB tích hợp với Active Directory (AD) để xác thực người dùng.

### 🍃 FSx File Gateway
![[00 Meta/01 Attachments/Pasted image 20230323224430.png]]
- **Local cache những dữ liệu thường xuyên được truy cập**
- Tương thích với Window
- Hữu ích cho việc nhóm các file và làm thư mục home.

### 🍃 Volume Gateway
![[00 Meta/01 Attachments/Pasted image 20230323225014.png]]
- Sử dụng giao thức iCSI để giao tiếp giữa local và Volume Gateway
- EBS snapshots có thể giúp restore dữ liệu 'mặt đất'.
- **Cached volumes:** độ trễ thấp khi truy cập dữ liệu thường xuyên.
- **Stored volumes:** lưu trữ được toàn bộ dữ liệu 'mặt đất', sắp lịch để backups dữ liệu vào S3.

### 🍃 Tape Gateway
![[00 Meta/01 Attachments/Pasted image 20230323225348.png]]
- Với một số công ty vẫn thực hiện việc sao chép dữ liệu trên đĩa từ, có thể sử dụng option này. Luồng thì vẫn như trên, dữ liệu vẫn sẽ được lưu trữ trên cloud.
- Dữ liệu trên S3 sẽ được lưu trữ trong Amazon Glacier hoặc Glacier Deep Archive.


## 🌿 Hardware appliance
![[00 Meta/01 Attachments/Pasted image 20230323225827.png]]
- Với 4 options trên, chúng ta đều sẽ cài các gateway trên máy ảo ở dưới local để sử dụng. Nhưng nếu chúng ta không có đủ tài nguyên để add thêm một gateway, chúng ta có thể thuê hardware của AWS, sau đó cài gateway lên đấy.
- Hoạt động với 3 options trên trừ S3 File Gateway.
- Hữu ích cho việc backup hàng ngày hệ thống NFS ở những data centers nhỏ.

## 🌿 Summary
![[00 Meta/01 Attachments/Pasted image 20230323230247.png]]