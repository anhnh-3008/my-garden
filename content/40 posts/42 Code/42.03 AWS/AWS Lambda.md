---
title: "🌱 AWS Lambda"
tags: [aws]
date: 2023-03-27
alias: [lambda]
---

## 🌿 What?
- Là một dịch vụ tính toán không máy chủ được cung cấp bởi AWS.
- Cho phép run code mà không cần chúng ta phải cung cấp hay quản lý servers.

## 🌿 Why?
- **Virtual Functions - không cần quản lý server.**
- **Giới hạn thời gian excute**
- **Run on-demand(chạy theo yêu cầu), có yêu cầu gửi đến thì mới chạy. Còn như EC2 là chạy bất kể ngày đêm, chỉ trừ khi chúng tắt**
- **Tự động mở rộng một cách mượt mà, không giống EC2 phải xóa add/remove servers**

## 🌿 Benefits of AWS Lambda
- Dễ dàng thanh toán:
	- Trả theo từng request và thời gian compute
	- Free tier cung cấp 1,000,000 AWS Lambda requests và 400,000 GBs thời gian compute
- Tích hợp được với toàn bộ các services của AWS.
- Tích hợp được với nhiều ngôn ngữ lập trình.
- Dễ dàng giám sát chỉ số thông qua AWS CloudWatch
- Dễ dàng lấy thêm tài nguyên cho từng funtions(up to 10GB RAM)
- Khi tăng RAM tự động cũng sẽ phát triển cả CPU và network!

## 🌿 Language support
- Node
- Python
- Java(tương thích Java 8)
- C#(.NET Core)
- Golang
- C# / Powershell
- Ruby
- Custom Runtime API
- Lambda Container Image

## 🌿 Pricing
- Pay per **calls**:
	- 1,000,000 requests đầu tiên sẽ được miễn phí.
	- 0.2$ cho mỗi 1,000,000 requests tiếp theo.
- Pay per **duration**:
	- 400,000 GB-seconds thời gian tính toán trong một tháng - free
	- = 400,000 seconds ứng với function là 1GB RAM.
	- = 3,200,000 seconds ứng với 1288 MB RAM
- Rất rẻ để chạy AWS Lambda nên nó rất rất phổ biến!

## 🌿 Invoking from RDS & Aurora
- Trong thực tế, có những trường hợp chúng ta cần gọi Lambda Funtions từ trong DB instance để thực hiện một tác vụ gì đó (ví dụ như khi người dùng insert một bản ghi vào RDS -> RDS gọi Lambda để Lambda gửi email xác nhận tới người dùng)
- Cho phép chúng ta thực hiện các data events từ trong một databases.
- Hỗ trợ với **RDS for PostgreSQL và Aurora MySQL**.
- **Phải cho phép outbound traffic của DB instance tới Lambda function**.
- **DB instance cần phải yêu cầu quyền để gọi Lambda funtion**.(Lambda Resource-based Policy & IAM Policy)
![[00 Meta/01 Attachments/Pasted image 20230328213427.png]]

- RDS Event Notifications
	- Chỉ gửi event về trạng thái hoạt động của database(created, stopped, start,...), sẽ không gửi thông tin về dữ liệu.
	- Đăng ký để theo dõi các event của: **DB Instance, DB snapshot, DB Parameter Group, DB Security Group, RDS Proxy, Custom Engine Version.**
	- Gần với thời gian thực(chậm nhất là 5p có thông báo)

