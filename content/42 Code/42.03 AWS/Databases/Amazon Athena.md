---
title: "🌱 Amazon Athena"
tags: [aws]
date: 2023-04-05
alias: [athena]
---

## 🌿 What?
- Là dịch vụ query **[[42 Code/42.03 AWS/Some Solution Architectures/Serverless|serverless]]**, dùng để phân tích dữ liệu trong [[42 Code/42.03 AWS/S3|S3]].
- Sử dụng ngôn ngữ SQL tiêu chuẩn để query files(built trên Presto).
- Hỗ trợ các định dạng CSV, JSON, ORC, Avro, và Parquet.
- Giá: 5$ trên một TB dữ liệu scan.
- Thường được kết hợp với một dịch vụ khác là Amazon QuickSight để báo cáo hoặc làm dashboard.

- **Use cases:** Phân tích/ báo cáo, **CloudTrail trails**, ...
- **Nói chung là muốn phân tích dữ liệu lưu trong [[42 Code/42.03 AWS/S3|S3]] bằng [[42 Code/42.03 AWS/Some Solution Architectures/Serverless|serverless]] SQL thì sử dụng Athena.**

## 🌿  Performance Improvement
- Sử dụng **columnar data** khi chỉ muốn scan đúng cột chúng ta cần.(less scan)
	- Tiết kiệm chi phí
- **Compress data** cho những truy suất nhỏ hơn
- **Partition** datasets trong [[42 Code/42.03 AWS/S3|S3]], giúp query dễ dàng hơn trên các cột ảo.
- **Use larger files**(> 128MB) để tối thiểu overhead(truyền tải tốt hơn).

## 🌿  Federated Query
- Athena cho phép chúng ta chạy SQL queries cho cả những dự liệu được lưu trữ dưới dạng relational, non-relational, object và custom data sources(AWS hoặc on-premises)
- Sử dụng **Data Source Connectors**([[42 Code/42.03 AWS/AWS Lambda|AWS Lambda]]) để chạy Federated Queries(queries tới CloudWatch Logs, [[42 Code/42.03 AWS/Databases/Amazon DynamoDB|DynamoDB]], [[42 Code/42.03 AWS/Databases/Amazon RDS - Relational Database Service|RDS]], ...)
- Lưu trữ kết quả phân tích được vào lại [[42 Code/42.03 AWS/S3|S3]].