---
title: "🌱 Big Data Ingestion Pipeline"
tags: [aws]
date: 2023-04-05
---

## 🌿 Requirements
- [[40 posts/42 Code/42.03 AWS/Some Solution Architectures/Serverless|Serverless]]
- Muốn thu thập dữ liệu real-time
- Muốn chuyển đổi dữ liệu
- Muốn truy vấn dữ liệu đã qua chuyển đổi bằng SQL
- Các báo cáo được tạo ra từ truy vấn cho [[40 posts/42 Code/42.03 AWS/S3|S3]].
- Muốn load dữ liệu vào một warehouse và tạo dashboard.

## 🌿 Architecture
![[00 Meta/01 Attachments/Pasted image 20230405235737.png]]
- [[40 posts/42 Code/42.03 AWS/Some Solution Architectures/Serverless|Serverless]]
	- [[40 posts/42 Code/42.03 AWS/Amazon Kinesis|Kinesis]] Data Streams: real-time
	- [[40 posts/42 Code/42.03 AWS/Amazon Kinesis|Kinesis]] Data Firehose: giúp delivery dữ liệu gần real-time(1 phút)
	- [[40 posts/42 Code/42.03 AWS/S3|S3]]: lưu trữ
	- [[40 posts/42 Code/42.03 AWS/AWS Lambda|Lambda]]: chuyển đổi dữ liệu
	- [[40 posts/42 Code/42.03 AWS/Databases/Amazon Athena|Athena]]: truy vấn dữ liệu đã qua chuyển đổi
	- [[40 posts/42 Code/42.03 AWS/Redshift|Redshift]] -> [[40 posts/42 Code/42.03 AWS/Amazon QuickSight|QuickSight]]: tạo báo cáo, load vào warehouse và tạo dashborad.


