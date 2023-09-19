---
title: "🌱 AWS KMS - Key Management Service"
tags: [aws]
date: 2023-04-15
alias: [kms]
---

## 🌿 What?
- Là dịch vụ lưu trữ keys encrypt trên AWS.
- Bất cứ khi nào nhắc về encrypt, hầu hết sẽ đề cập đến KMS.
- Được tích hợp với IAM để thực hiện authorization.
- Giúp việc quản lý truy cập dữ liệu dễ dàng hơn.
- Có thể audit các KMS keys được sử dụng ntn thông qua [[40123345 posts/42 Code/42.03 AWS/Monitoring/Amazon CloudTrail|CloudTrail]].
- Có khả năng tích hợp với nhiều services của AWS như [[40123345 posts/42 Code/42.03 AWS/Databases/Amazon RDS - Relational Database Service|RDS]], [[40123345 posts/42 Code/42.03 AWS/S3|S3]], [[40123345 posts/42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]], ...
- **Không bao giờ được lưu trữ các khóa bằng text thường, đặc biệt là ở trong code, lưu trong biến môi trường thôi.**

## 🌿 Types
- **KMS Key có tên mới là KSM Customer Master Key**
- **Symmetric(AES-256 keys)**
	- Một khóa duy nhất dùng cả cho encrypt và decrypt
	- Các services AWS sẽ được tích hợp trực tiếp với KMS để sử dụng Symmetric key.
	- Chúng ta sẽ không thể truy cập được vào Symmetric Key để lấy dữ liệu unencrypt(bắt buộc phải thông qua API của KMS)
- **Asymmetric(RSA & ECC key pair)**
	- Có một cặp khóa public/private, khóa public để encrypt, khóa private để decrypt.
	- Public key chúng ta có thể download và lưu trữ được, còn private thì không.
	- Sử dụng với các trường hợp người dùng không thể call API của KMS.

## 🌿 Policies
- Kiểm soát truy cập tới các KMS Keys.
- **Default KMS Key Policy**
	- Được tạo nếu chúng ta không chỉ địng policy nào.
	- Cho phép toàn bộ AWS accounts truy cập
- **Custom KMS Key Policy**
	- Xác định users, roles nào được truy cập vào KMS Key.
	- Xác định quản trị viên cho KMS Key.
	- Phù hợp để sử dụng với trường hợp xài chung cho nhiều accounts.

## 🌿 Multi-Region Key
- Một khóa chính và được nhân rộng(sao chép) khóa cho các regions còn lại.
- Giúp dễ dàng quản lý key, giảm thiểu thao tác tạo key trên nhiều region. 
- Sử dụng với các service trên nhiều region vd như Global [[40123345 posts/42 Code/42.03 AWS/Databases/Amazon DynamoDB|DynamoDB]], Global Aurora...