---
title: "🌱 Event Processing in AWS"
tags: [aws, architecture]
date: 2023-04-21
---

> Bài viết tổng hợp lại các kiến trúc thường được áp dụng cho hệ thống xử lý sự kiện trên AWS.

## 🌿 Lambda, SNS and SQS
Có 3 kiến trúc thường được sử dụng:
1. SQS + Lambda
![[00 Meta/01 Attachments/Pasted image 20230421210356.png]]
- Events push vào SQS queue
- Lambda pull mess từ SQS về để xử lý, nếu xử lý không thành công thì push ngược trở lại SQS.
- Tránh trường hợp message có vấn đề, mãi không được xử lý thành công, gây ra vòng lặp vô hạn -> Chuyển message vào DLQ(Dead Letter Queue) sau số lần retry nhất định, không xử lý nó nữa

2. SQS FIFO + Lambda
![[00 Meta/01 Attachments/Pasted image 20230421210929.png]]
- Giống cái bên trên, khác là các messages trong Queue có thứ tự FIFO - First In First Out.

3. SNS + Lambda
![[00 Meta/01 Attachments/Pasted image 20230421211044.png]]
- Notification đc gửi bất đồng bộ tới Lambda để xử lý.
- Luồng retry + đẩy vào DLQ giống 2 cái bên trên.

## 🌿 Fan Out Pattern - delivery to multi SQS
![[00 Meta/01 Attachments/Pasted image 20230421211812.png]]
- Fan Out Pattern: được sử dụng với mục đích phân phối thông điệp tới nhiều đối tượng cùng lúc.
- Đảm bảo tính đúng đắn và tin cậy của các thông điệp.
- Tăng khả năng chịu lỗi.
- Có khả năng mở rộng linh hoạt.
- Sử dụng SNS - SNS hỗ trợ nhiều định dạng như email, tin nhắn, văn bản, ... Tùy nhu cầu chúng ta có thể lựa chọn 2 options trên.

- Option1:
	- Cơ chế sẽ là một message sẽ được put lần lượt tới các Queue
	- Nhưng có thể xảy ra trường hợp put Queue2, message bị lỗi, thế là nó ko put đến Queue3 nữa -> Không đáng tin cậy
- Option2:
	- Tăng cường độ tin cậy bằng cách thông qua SNS, kiêu gì nó cũng gửi message lên cả 3 Queue.

## 🌿 Events of S3

### 🍃 With EventBridge
![[00 Meta/01 Attachments/Pasted image 20230424202403.png]]
- **Filter Advance** - có thể tạo JSON rules, hỗ trợ cho việc tìm kiếm các thông tin của objects(metadata, size, ...)
- **Multiple Destinations** - Có thể gửi các event tới nhiều AWS services khác, dễ dàng xử lý nhiều tác vụ theo nhu cầu sử dụng của hệ thống.
- **Capabilities** - Ngoài ra EventBridge hỗ trợ lưu trữ, replay event, reliable delivery

![[00 Meta/01 Attachments/Pasted image 20230424202857.png]]
- Ngoài ra nó còn được sử dụng để nhận các events từ các API được call. Từ đó có thể gửi tới các service khác ví dụ như SNS trong trường hợp khi người dùng xoá một bảng sẽ gửi mail tới tất cả các AWS accounts trong organization.

### 🍃 With API Gateway
![[00 Meta/01 Attachments/Pasted image 20230424203103.png]]
- Mô hình thường được sử dụng để người dùng có thể lưu dữ liệu lên S3.