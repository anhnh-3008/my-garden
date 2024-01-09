---
title: "🌱 AWS Global Accelerator"
tags: [aws]
date: 2023-03-21
---

## 🌿 Vấn đề
![[00 Meta/01 Attachments/Pasted image 20230321222308.png]]
- Chúng ta có một server app đặt tại một region, và người dùng của app là khắp nơi trên thế giới.
- Họ đến public internet và điều này sẽ gây ra độ trễ lớn từ nhiều bước truyền dữ liệu.
- Chúng ta muốn dữ liệu được truyền nhanh nhất có thể thống AWS network với độ trễ tối thiểu.

## 🌿 Unicast IP và Anycast IP
- **Unicast IP:** mỗi server có một địa chỉ IP riêng
- **Anycast IP:** tất cả server đều có IP giống nhau và user sẽ được định tuyến đến server gần nhất.

## 🌿 How
- Tận dụng mạng nội bộ của AWS để định tuyến tới app của bạn.
- **2 Anycast IP** được tạo cho app của chúng ta.
- Anycast IP gửi lượng truy cập trực tiếp tới các edge locations và edge locations sẽ gửi lượng truy cập về app của chúng ta.

- Works với **Elastic IP, EC2 Instance, ALB, NLB, public hoặc private**
- Hiệu suất nhất quán.
	- Định tuyến thông minh để có độ trễ thấp nhất và khả năng chuyển đổi dự phòng region nhanh nhất.
	- Không ảnh hưởng đến client cache(bởi vì IP không đổi)
	- Sử dụng mạng nội bộ của AWS
- Health Checks
	- Có thực hiện health check với app của chúng ta.
	- Giúp app của chúng ta được global(có khả năng chuyển đổi dự phòng dưới một phút nếu app bị đánh giá unhealthy)
	- Phù hợp cho TH phục hồi sau thảm họa.
- Security
	- Chỉ được cho phép 2 IP nội bộ truy cập.
	- Có DDoS nhờ có thằng AWS Shield
