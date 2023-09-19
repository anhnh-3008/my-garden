---
title: "🌱 AWS DataSync"
tags: [aws]
date: 2023-03-23
---

## 🌿 What?
- Dùng để move một số lượng lớn dữ liệu 
	- Từ mặt đất lên could
	- Từ service này -> service khác
- Có thể đồng bộ dữ liệu:
	- Amazon S3(với bất kỳ storage classes nào - bảo gồm cả Glacier)
	- Amazon EFS
	- [[40123345 posts/42 Code/42.03 AWS/Amazon FSx|Amazon FSx]]
- Các tasks nhân bản sẽ được đặt lịch hàng giờ/hàng ngày/hang tuần.
- **File permissions và metadata được giữ nguyên khi đồng bộ.**
- Một agent có thê sử dụng 10Gps, có thể setup giới hạn cho băng thông.

- Đồng bộ dữ liệu giữa on-premises và cloud:
![[00 Meta/01 Attachments/Pasted image 20230323233411.png]]

- Đồng bộ giữa các services:
![[00 Meta/01 Attachments/Pasted image 20230323233636.png]]
