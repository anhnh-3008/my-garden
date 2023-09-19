---
title: "🌱 Amazon OpenSearch Service"
tags: [aws]
date: 2023-04-05
alias: [opensearch]
---

## 🌿 What?
- Được kế thừa từ Amazon ElasticSearch, cung cấp khả năng tìm kiếm dữ liệu mạnh mẽ và linh hoạt trên AWS.
- Chúng ta có thể **tìm kiếm bất kỳ field nào thậm chí là cả tìm kiếm theo partially.**
- Thường được sử dụng như một phần bổ sung cho các database khác.
- OpenSearch yêu cầu một cụm các instances(không phải serverless).
- Không hỗ trợ sẵn SQL(có thể enabled thông qua plugin)
- Có thể tìm kiếm ở những services khác nhau như là Kinesis Data Firehose, AWS IoT và CloudWatch Logs.
- Bảo mật thông qua Cognito & IAM, mã hóa KMS, TLS.

- Có khả năng:
	- Xử lý ngôn ngữ tự nhiên
	- Tìm kiếm dữ liệu phân tán

## 🌿 Cấu trúc
- Cấu trúc thường được sử dụng với DynamoDB:
![[00 Meta/01 Attachments/Pasted image 20230405224454.png]]

- Cấu trúc thường được sử dụng với CloudWatch:
![[00 Meta/01 Attachments/Pasted image 20230405224608.png]]

- Cấu trúc thường được sử dụng với Kinesis Data Streams & Kinesis Data Firehose:
![[00 Meta/01 Attachments/Pasted image 20230405224730.png]]
