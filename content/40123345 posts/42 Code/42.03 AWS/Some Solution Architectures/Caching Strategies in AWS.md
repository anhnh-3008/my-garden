---
title: "🌱 Caching Strategies in AWS"
tags: [aws]
date: 2023-04-24
alias: [caching strategies]
---

![[00 Meta/01 Attachments/Pasted image 20230424204731.png]]
- AWS cũng cấp nhiều dịch vụ hỗ trợ caching.
- Việc lựa chọn dịch vụ caching một cách hiệu quả sẽ liên quan rất nhiều đến cách thức hoạt động của hệ thống.
- Ví dụ nếu app yêu cầu độ trễ thấp, không cần đồng bộ real-time dữ liệu hoặc những thay đổi từ bên BE, có thể lựa chọn CloudFront để caching
- Cache trên từng khu vực thì có thể chọn [[40123345 posts/42 Code/42.03 AWS/AWS API Gateway|API Gateway]].
- Với app nào mà không quan tâm đến độ trễ lắm, nhưng cần dữ liệu phải có tính thống nhất cao thì có thể sử dụng cache ở [[40123345 posts/42 Code/42.03 AWS/Databases/Amazon ElastiCache|ElastiCache]], DAX.
- Nói chung là có nhiều dịch vụ hỗ trợ caching, cần phải làm rõ được các yêu cầu như về độ trễ, thời gian lưu trữ, giá cả, ... để chọn được cách hoạt động hiệu quả nhất cho dự án.
