---
title: "🌱 Amazon Glue"
tags: [aws]
date: 2023-04-05
alias: [glue]
---

## 🌿 What?
- Là dịch vụ ETL(Extract, transform và load)
- Hữu ích để chuẩn bị và chuyển đổi dữ liệu để phân tích.
- **[[42 Code/42.03 AWS/Some Solution Architectures/Serverless|serverless]]**
![[00 Meta/01 Attachments/Pasted image 20230405232846.png]]

- **Glue Job Bookmarks:** ngăn ngừa việc xử lý lại dữ liệu cũ.
- **Glue Elastic Views:**
	- Kết hợp và sao chép dữ liệu trên nhiều dữ liệu lưu trữ bằng SQL.
	- Không custom code, Glue quan sát những thay đổi trong source data, serverless.
	- Tạn dụng một bảng ảo.
- **Glue DataBrew:** làm sạch và chuẩn hóa dữ liệu sử dụng pre-built transformation.
- **Glue Studio:** GUI mới để tạo, chạy và quan sát ETL jobs trong Glue.
- **Glue Stream ETL:** tương thích với Kinesis Data Streaming, Kafka, MSK.
