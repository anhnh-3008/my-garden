---
title: "🌱 Amazon CloudWatch"
tags: [aws]
date: 2023-04-08
alias: [cloudwatch]
---

## 🌿 What?
- Là một dịch vụ giám sát, ghi log và cảnh báo trên môi trường cloud của AWS. Nó giúp chúng ta giám sát tài nguyên và ứng dụng trên AWS, thu thập và phân tích các dữ liệu khác nhau, cung cấp các thông tin về hoạt động và hiệu suất của các tài nguyên và ứng dụng của chúng ta.

## 🌿 CloudWatch Metrics
- Là tính năng của CloudWatch cung cấp các thông số hiệu suất hoạt động của tất cả các services của AWS.
- **Metric** là một biến để giám sát(CPUUtilization, network, ...)
- Các Metrics thuộc về các **namespaces**.
- **Dimension** là một thuộc tính của một metric(instance id, environment, ...)
- Tối đa là 30 dimensions cho từng metric.
- Các metrics đều có **timestamps**.
- Có thể tạo CloudWatcch dashboards từ các metrics.
- Có thể tạo **CloudWatch Custom Metrics** để trích xuất dữ liệu cần thiết(ví dụ như trích xuất metric của RAM của EC2 instance, ...)

### 🌱 Streams
- Có thể liên tục stream các thông số hiệu suất của app tới các destinations khác để thực hiện các tác vụ như lưu trữ, phân tích ... với tần suất **near-real-time** và độ trễ thấp.
- Có thể lựa chọn **filters metrics** để chỉ định stream tới destinations.
![[00 Meta/01 Attachments/Pasted image 20230408140045.png]]

## 🌿 CloudWatch Logs
- Là tính năng của CloudWatch giúp chúng ta lưu trữ Logs của hệ thống.
- **Log groups**: thường là đại diện cho một app.
- **Log stream:** instances bên trong app / log files / containers.
- Có thể xác định thời gian hết hạn của log(nerver, 30 days, ...), sau thời gian hết hạn, log sẽ tự động được xóa. Chúng ta sẽ phải trả tiền để được lưu log trên AWS.
- **CloudWatch Logs có thể gửi logs tới:**
	- Amazon [[40 posts/42 Code/42.03 AWS/S3|S3]]
	- [[40 posts/42 Code/42.03 AWS/Amazon Kinesis|Kinesis]] Data Streams
	- [[40 posts/42 Code/42.03 AWS/Amazon Kinesis|Kinesis]] Data Firehose
	- AWS [[40 posts/42 Code/42.03 AWS/AWS Lambda|Lambda]]
	- [[40 posts/42 Code/42.03 AWS/Amazon OpenSearch Service|OpenSearch]]

### 🌱 Filter & Insights
- Có thể filter để xem log dễ dàng hơn.
- Metric filters có thể được sử dụng để trigger CloudWatch alarms.
- CloudWatch Logs Insight có thể được sử dụng để query logs và thêm các câu queries để làm Dashboards.

### 🌱 Log Subcriptions
- Dùng **Subcription Filter** để điều hướng đến các dịch vụ tùy theo nhu cầu sử dụng của dự án.
![[00 Meta/01 Attachments/Pasted image 20230408141720.png]]

- Kiến trúc để thu thập logs từ nhiều accounts, regions về một chỗ:
![[00 Meta/01 Attachments/Pasted image 20230408141817.png]]

## 🌿 Agent & Logs Agent
- Mặc định sẽ không có logs từ EC2 machine tới CloudWatch. Để thu thập logs của EC2, chúng ta cần tạo một CloudWatch Agent đặt trong EC2 và nó sẽ thu thập + push log lên CloudWatch.
- Lưu ý về IAM permissions.
- CloudWatch log agent có thể setup được cả ở những server on-premises
![[00 Meta/01 Attachments/Pasted image 20230408144534.png]]

## 🌿 Alarms
- Là dịch vụ dùng để trigger các thông báo của các metrics.
- Có nhiều options(sampling, % max, min, ...) để thực hiện trigger
- Alarm States:
	- OK
	- INSUFFICIENT_DATA
	- ALARM
- Period - thời gian tính theo giây, để đánh giá metric.
	- có thể custom: 10s, 30s hoặc nhiều lần 60s.
- Targets - đối tượng trigger của alarms:
	- Stop, Terminate, Reboot hoặc Recover EC2 Instance.
	- Trigger đến Auto Scaling Action.
	- Gửi thông báo đến [[40 posts/42 Code/42.03 AWS/Amazon SNS - Simple Notification Service|SNS]].

### 🌱 Composite Alarms
- CloudWatch Alarms là một metric đơn lẻ.
- Composite alarms sẽ giúp chúng ta giám sát được trạng thái của nhiều alarms khác nhau.
- Có thể kết hợp điều kiện AND hoặc OR để kết hợp các alarms, tránh gặp những alarm noise không cần thiết.
	- Ví dụ high CPU và high Network là bình thường, mình chỉ cần nó alarm lúc bất thường như high CPU những low Network. Đó chính là tác dụng của Composite Alarms.

- Alarms có thể được tạo dự trên CloudWatch Logs Metrics Filters.

## 🌿 Insight
- **Container insight:**
	- Trích xuất, tổng hợp logs và metrics của các container trong AWS, sử dụng CloudWatch Agent.
- **Lambda insight:**
	- Trích xuất, tổng hợp logs và metrics cho các ứng dụng có kiến trúc serverless.
- **Contributes insight:**
	- Cung cấp các thông tin chi tiết, dễ dàng tìm kiếm các thông số có giá trị bất thường.
- **Application insight:**
	- Tự động tạo bảng thống kê, phản ánh các vấn đề của hệ thống hoặc của các AWS services.


