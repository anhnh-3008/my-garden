---
title: "🌱 AWS Secrets Manager"
tags: [aws]
date: 2023-04-16
alias: [secrets manager]
---

## 🌿 What?
- Là dịch vụ lưu trữ và quản lý các thông tin bí mật của app(thông tin connect vào database, khóa mã hóa dữ liệu, ...)
- Dịch vụ này sẽ chịu trách nhiệm lưu trữ, bảo mật và cung cấp cho các dịch vụ tích hợp những thông tin bí mật này một cách an toàn.
- Các thông tin bảo mật được lưu trữ trong dịch vụ hoàn toàn được mã hóa bằng KMS.
- Có khả năng quản lý vòng đời của các thông tin bí mật này.
- Thường sẽ được sử dụng để tích hợp với RDS.

## 🌿 Multi-Region Secrets
- Tính năng cho phép sao chép, nhân rộng Secret Manager trên nhiều Region.
- Bao gồm một Secret Manager chính, các Secret Manager trên region khác sẽ được đồng bộ.
- Có thể promote một Secret Manager trên region khác trở thành một phiên bản độc lập.
![[00 Meta/01 Attachments/Pasted image 20230416003249.png]]
