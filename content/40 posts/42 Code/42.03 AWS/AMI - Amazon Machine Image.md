
---
title: "🌱 AMI - Amazon Machine Image"
tags: [aws]
date: 2023-03-04
---

## 🌿 What?
- AMI - Amazon Machine Image
- Có chứa những thông tin về OS, phần mềm cài đặt, volumes, cấu hình, hay các thiết lập khác của một EC2 Instance.
	- Dễ dàng triển khai. Nhất quán về cấu hình cũng như  thiết lập của các EC2 Instances.
	- Fast boot vì Image đã được chuẩn bị trước về phần mềm cài đặt, thiết lập, ...
- AMI thuộc về một Region chỉ định( chúng ta có thể copy để sử dụng ở những Region khác)
- Các Options để có một AMI:
	- A public AMI: AWS cung cấp một số AMI mẫu, mỳ ăn liền.
	- Your own AMI: tự tạo và thiết lập để phù hợp với nhu cầu sử dụng của bản thân.
	- An AWS Marketplace AMI: Có thể mua/bán AMI trên market. Có thể khởi nghiệp bằng công việc bán AMI luôn 😍

## 🌿 AMI Process( từ một EC2 Instance)
- Tạo một EC2 Instance và tùy chỉnh nó.
- Dừng Instance(Data được toàn vẹn)
- Tạo AMI - Giống tạo EBS snapshots
- Launch Instance từ AMIs
