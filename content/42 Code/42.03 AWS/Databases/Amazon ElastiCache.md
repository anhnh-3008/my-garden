---
title: "🌱 Amazon ElastiCache"
tags: [aws]
date: 2023-03-09
alias: [elasticache]
---

## 🌿 What?
- Dịch vụ lưu cache của Amazon, hỗ trợ Redis hoặc Memcached.
- Cache mang lại hiệu suất cao(dữ liệu cần đã có sẵn, chỉ việc lấy ra dùng), đỗ trễ thấp.
- Giảm thiểu số lượng queris đọc vào database.
- Giống RDS, Amazon sẽ takes care OS, patching, optimizations, setup configuration, monitoring, failure recovery and backups.
- **Sử dụng ElastiCache sẽ phải thêm code.**

## 🌿 Redis vs Memcached
|Redis|Memcached|
|------|------------|
|**Multi-AZ** và tự động chuyển đổi dự phòng|Multi-node để phân vùng dữ liệu|
|**Read replicas** để scale đọc và **high availability**| Không High Availibility|
|Dữ liệu bền - persistence| Dữ liệu không bền|
|**Có chức năng Backup và Restore**| Không có|
|Hỗ trợ Sets và Sorted Sets| Kiến trúc đa luồng|

## 🌿 Security
- **IAM Authentication for Redis**, chỉ được dùng với AWS API-level security
- **Redis AUTH**
	- set một cặp "password/token" khi tạo một cụm Redis cluster mới
- **Memcached**
	- hỗ trợ SASL.

## 🌿 Patterns
- **Lazy Loading**
- **Write Through**
- **Session Store**

## 🌿 Use Case
- Xếp hạng Gaming, cần tính toán phức tạp. **Redis Sorted** đảm bảo tính uniq cũng như thứ hạng của elements.