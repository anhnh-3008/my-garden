---
title: "🌱 Serverless Architectures - Myblog.com"
tags: [aws]
date: 2023-03-31
---

## 🌿 Requirements
- Một web viết blog có khả năng mở rộng toàn cầu.
- Các bài blogs hiếm khi được viết nhưng thường hay được đọc.
- Caching
- Khi người dùng mới đăng ký phải gửi một email chào mừng người dùng.
- Khi có ảnh được upload sẽ tự động tạo thumbnail.

## 🌿 Architecture
![[00 Meta/01 Attachments/Pasted image 20230331162606.png]]

- Vẫn sử dụng kiến trúc [[40 posts/42 Code/42.03 AWS/AWS API Gateway|API Gateway]] + [[40 posts/42 Code/42.03 AWS/AWS Lambda|Lambda]] + DAX + [[40123345 posts/42 Code/42.03 AWS/Amazon DynamoDB|DynamoDB]] để đáp ứng yêu cầu như expose API HTTP, truy vấn các bài posts tăng hiệu suất đọc dữ liệu.
- Để app global, sử dụng CloudFront để phân phối. Các edge location sẽ nhận request của người dùng, giảm độ trễ, nâng cao trải nghiệm của người dùng.
- [[40 posts/42 Code/42.03 AWS/S3|S3]] thiết lập OAC - Origin Access Control để các edge location có thể truy cập được vào [[40 posts/42 Code/42.03 AWS/S3|S3]].
- Tiếp đến là vụ gửi mail. Bật [[40123345 posts/42 Code/42.03 AWS/Amazon DynamoDB|DynamoDB]] Stream để nhận được sự kiện khi có người dùng được tạo mới trong db. Sau đó dùng [[40 posts/42 Code/42.03 AWS/AWS Lambda|Lambda]] để thực hiện gửi mail qua dịch vụ Simple Email Service(SES)
- Về vụ gen ra thumbnail, sau khi ảnh được upload vào [[40 posts/42 Code/42.03 AWS/S3|S3]], gửi sử kiện đến [[40 posts/42 Code/42.03 AWS/AWS Lambda|Lambda]] để tạo thumbnail và import vào [[40 posts/42 Code/42.03 AWS/S3|S3]].
