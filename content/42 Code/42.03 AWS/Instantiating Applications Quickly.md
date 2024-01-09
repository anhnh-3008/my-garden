---
title: "🌱 Instantiating Applications Quickly"
tags: [aws]
date: 2023-03-12
---

- Thông thường, khởi chạy một app chúng ta sẽ thường chạy stack sau: EC2 instance, EBS, RDS, làm thế nào để tăng tốc khởi chạy stack này?
- EC2 Instance:
	- Sử dụng **Golden AMI** - Là Image đã thực hiện install packages cũng như config từ trước rồi, giúp tăng tốc trong việc khởi chạy một instance mới.
	- **Bootstrap User Data** - Sử dụng User Data để thực hiện các tác vụ config động.
	- **Hybrid** Kết hợp giữa **Golden AMI** và **User Data** (Elastic Beanstalk)
- EBS vs RDS:
	- Lưu trữ snapshot để thực hiện restore nhanh chóng 
