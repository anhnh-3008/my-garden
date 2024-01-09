---
title: "🌱 EC2 Instance Store"
tags: [aws]
date: 2023-03-04
---

## 🌿 What?
- Cho phép lưu trữ dữ liệu của 1 EC2 Instance ở trên một ổ đĩa vật lý, được đặt cùng với máy chủ chứa Instance.
- Khác với EBS Volume lưu trữ và truy xuất dữ liệu thông qua mạng, EC2 Instance Store có một đặc điểm sau:
	- I/O performance tốt hơn EBS Volume
	- Giảm thiểu khả năng xảy ra do sự cố mạng và hao tổn băng thông. Nhưng có khả năng bị mất dữ liệu do hardware xảy ra lỗi.
	- Mất dữ liệu khi EC2 Instance bị dừng hoặc xóa.
	- Nên sử dụng với những ứng dụng không cần lưu trữ dữ liệu dài hạn hoặc không thì cần phải thực hiện lưu trữ và backup bằng những dịch vụ khác.
- Cân nhắc giữa EC2 Instance và EBS Volume để có lựa chọn phù hợp nhất với dự án.

