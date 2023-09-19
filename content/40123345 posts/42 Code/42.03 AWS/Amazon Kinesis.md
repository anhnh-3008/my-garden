---
title: "🌱 Amazon Kinesis"
tags: [aws]
date: 2023-03-25
alias: [kinesis]
---

## 🌿 What?
- Là dịch vụ giúp chúng ta đơn giản hóa việc **thu thập, xử lý cũng như là phân tích** luồng dữ liệu một cách realtime.

- Có 4 loại:
	- **Kinesis Data Streams:** capture, xử lý và lưu trữ data streams.
	- **Kinesis Data Firehose:** load data streams vào các dịch vụ lưu trữ của AWS.
	- **Kinesis Data Analytics:** phân tích data streams cùng với SQL hoặc Apache Flick
	- **Kinesis Video Streams:** capture, xử lý và lưu trữ video streams.
![[00 Meta/01 Attachments/Pasted image 20230325212843.png]]

## 🌿  Kinesis Data Streams
![[00 Meta/01 Attachments/Pasted image 20230325213658.png]]
- Giữ lại dữ liệu từ 1 -> 365 ngày.
- Có khả năng xử lý lại dữ liệu.
- Một khi dữ liệu được inserted vào Kinesis thì sẽ không thể xóa.
- Data được chia sẻ chung một partition thì sẽ vào chung một shard.
- Producers: AWS SDK, Kinesis Producer(KPL)
- Consumers:
	- KCL - Kinesis Client Library, AWS SDK
	- AWS Lambda, Kinesis Data Firehose, Kinesis Data Analytics.

### 🍃 Capacity modes
- **Provisioned mode**
	- Chúng ta được chọn số lượng shards, scale thủ công hoặc sử dụng API
	- Mỗi shard là 1MB/s in (1000 records mỗi giây)
	- Mỗi shard là 2MB/s out.
	- Thanh toán cho từng shard theo giờ.
- **On-demand mode**
	- Không cần khả năng cung cấp hoặc quản lý.
	- Mặc định 4MB/s
	- Tự động scale dựa vào thông lượng được quan sát trong 30 ngày gần nhất.
	- Trả tiền theo giờ từng stream, dữ liệu in/out per GB

- Nếu không có yêu cầu gì đặc biệt thì chọn **on-demand mode** dùng cho thuận tiện.

## 🌿 Kinesis Data Firehose
![[00 Meta/01 Attachments/Pasted image 20230325215757.png]]
- Dịch vụ toàn quyền sử lý, khong admin, tự động scale, serverless, giúp chuyển dữ liệu lớn vào storage tier.
- Trả tiền theo dữ liệu được truyền đến Firehose.
- **Gần real time.**
- Không lưu trữ dữ liệu.
- Không hỗ trợ khả năng replay.

## 🌿 Ordering data
- Giả sử app của chúng ta cần thực hiện check vị trí của các xe tải. Số lượng xe tải ngày càng tăng nếu tất cả dữ liệu được đổ vào các shards khác nhau trên Kinesis -> Mất dữ liệu hoặc mất thời gian để truy vấn dữ liệu.
- Giải pháp: Trong Kinesis, muốn dữ liệu được sắp xếp có thứ tự, sử dụng **partition key**. Vd keys là trunk_1, trunk_2, ...
- Các dữ liệu cùng key sẽ được stream trong cùng shard -> dễ dàng tìm kiếm hơn, tránh bị lack mất dữ liệu
![[00 Meta/01 Attachments/Pasted image 20230326081953.png]]

## 🌿 Kinesis vs SQS ordering
- Giả sử chúng ta có 100 trucks, 5 shards và 1 SQS FIFO
- Với Kinesis Data Streams:
	- Trung bình mỗi shard sẽ chứa dữ liệu của 20 trucks
	- Các trucks sẽ được sắp xếp trong mỗi shard.
	- Tối đa có thể có 5 consumers chạy đồng thời.
	- Có thể nhận được dữ liệu lên tới 5MB/s
- SQS FIFO:
	- Chỉ có một Queue
	- Có 100 Group ID
	- Tối đa có thể có 100 consumers
	- Có thể nhận được 300 messages mỗi giây(hoặc 3000 nếu kết hợp sử dụng batching)


