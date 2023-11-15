---
title: "🌱 AWS Config"
tags: [aws]
date: 2023-04-09
alias: [aws config]
---

## 🌿 What?
- Là dịch vụ quản lý cầu hình, cung cấp khả năng theo dõi và kiểm soát cấu hình tài nguyên của các AWS services.
- Giúp kiểm tra cũng như tuân thủ các luật lệ cho mỗi account.
- Giúp lưu lại config và có thể thay đổi bất kỳ lúc nào.
- Các vấn đề có thể giải quyết với AWS Config:
	- Có cái truy cập SSH không được unsretricted truy vập vào sg không?
	- Buckets có bao nhiêu truy cập public?
- Có thể nhận được thông báo ([[40 posts/42 Code/42.03 AWS/Amazon SNS - Simple Notification Service|SNS]]) khi có bất kỳ thay đổi nào.
- AWS Config là một dịch vụ riêng trên từng region.
- Có thể tổng hợp các dịch vụ từ nhiều regions và accounts.
- Có thể lưu config vào [[40 posts/42 Code/42.03 AWS/S3|S3]] và dùng [[40 posts/42 Code/42.03 AWS/Databases/Amazon Athena|athena]] để phân tích dữ liệu.

## 🌿 Rules
- Rules có thể được sử dụng để đánh giá/ trigger:
	- Cho những config thay đổi.
	- and/or tại một thời điểm bất kỳ
**- Nó không được dùng với mục đích ngăn ngừa các actions có thể xảy ra.**
- Giá: 
	- không có free tier
	- 0.003$ cho từng config item lưu trên một region
	- 0.001$ cho từng rule đánh giá trên một region

