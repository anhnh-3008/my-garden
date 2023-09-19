---
title: "🌱 Direct Connect (DX)"
tags: [aws]
date: 2023-04-18
alias: [direct connect, dx]
---

## 🌿 What?
- Là dịch vụ cung cấp kết nối mạng riêng tư để kết nối giữa Data Center của chúng ta tới AWS.
- Để sử dụng chúng ta cần setup một Virtual Private Gateway trên VPC.
- DX giúp chúng ta vừa có thể kết nối public(như resources của S3) và private(EC2 Instances) trong cùng một kết nối.
- Mạng riêng tư này nó băng thông rộng, độ trễ thấp và độ tin cậy cao. Giúp nâng cao hiệu suất của hệ thống, trải nghiệm của người dùng.
- Use Cases:
	- Khi ứng dụng có dataset lớn và muốn sử dụng với giá thành thấp.
	- Trải nghiệm mạng đồng nhất, như là các ứng dụng realtime.
	- Hybrid Environments - có kết hợp giữa on-premise và cloud.
- Dữ liệu được truyền tải không mã hóa, nhưng nó private.

## 🌿 Diagram
![[00 Meta/01 Attachments/Pasted image 20230418213808.png]]

## 🌿 Direct Connection Gateway
- Nếu chúng ta muốn kết nối giữa nhiều VPC ở khác regions(same accounts), chúng ta cần setup thêm **Direct Connection Gateway**.
![[00 Meta/01 Attachments/Pasted image 20230418214044.png]]

## 🌿 Connection Types
- **Dedicated Connection - 1Gbs, 10Gbs, 100Gbs**
	- Cho một cái etherner vật lý luôn.
	- Order thông qua AWS, AWS sẽ liên hệ đến Partner để hỗ trợ lắp đặt
- **Hosted Connection - 50Mbps, 500 Mbps, 10Gps**
	- Kết nối được cung cấp do bên Partner của AWS.
	- Option này chúng ta có thể add hoặc remove dựa theo nhu cầu sử dụng.
	- Có thể tăng lên 1Gbs, 2, 5, 10.
- Thời gian để lắp đặt cái này khá lâu, thường mất tầm 1 tháng để có thể sử dụng được Direct Connection.
