---
title: "🌱 On-Premise strategies with AWS"
tags: [aws]
date: 2023-04-20
alias: []
---

## 🌿 Các chiến lược sử dụng để liên kết on-premise với cloud
- Có khả năng Download Amazon Linux 2 AMI như một VM.
- VM import/export
	- Có thể migrate hệ thống đã có vào EC2
	- Tạo một nơi để thực hiện DC trên máy ảo.
	- Có thể export ngược lại từ EC2 về on-premise.
- AWS Application Discovery Service
	- Tổng hợp các thông tin về on-premise servers để lên kế hoạch migrate.
	- Kiểm tra, giám sát với AWS Migration Hub.
- AWS Database Migration Service([[40 posts/42 Code/42.03 AWS/Disaster Recovery/DMS - Database Migration Service|DMS]])
	- Nhân bản, sao chép cơ sở dữ liệu từ on-premise lên cloud
	- Hỗ trợ đa dạng các kiểu databases.
- AWS Server Migration Service(SMS)
	- Cung cấp một cái live server thực hiện nhân bản, sao chép database từ on-premise lên cloud.
