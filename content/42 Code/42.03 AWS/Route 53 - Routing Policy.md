---
title: "🌱 Route 53 - Routing Policy"
tags: [aws]
date: 2023-03-11
---

## 🌿 What?
- Định nghĩa cách Route 53 phản hồi những câu truy vấn DNS.
- Đừng nhầm lẫn từ **routing**
	- Không giống routing của ALB, đấy là định tuyến lưu lượng truy vấn.
	- Routing của Route 53 chỉ chịu trách nhiệm phản hồi những truy vấn DNS thôi.

## 🌿 Types
- Có những loại policies sau:

### 🍃 Simple
- Tiêu biểu, định tuyến tới một resource đơn lẻ.
- Có thể chỉ định nhiều values cho một record.
- **Nếu có nhiều values trả về, client sẽ pick ngẫu nhiên một value để thực hiện truy cập.**
- Khi bật Alias, phải chỉ định tới một resouce duy nhất.
- Không liên quan tới Health Check.

### 🍃 Weighted - tỉ trọng
- Kiểm soát phần trăm nhận requests được chỉ định cho từng resource.
- Các DNS records phải cùng tên và cùng kiểu.
- Có liên quan đến Health Check
- Use cases: Load balancing giữa các region, testing version mới của ứng dụng, ...
- Assign 0% cho một record, tức là resource đó sẽ không được gửi traffic.
- Nếu tất cả record được set = 0, thì sẽ trả về trọng số bằng nhau cho tất cả các records.

### 🍃 Latency based
- Chuyển hướng tới resource có độ trễ thấp nhất đối với client. Phù hợp với những ứng dụng mà độ trễ được ưu tiên.
- Vd client ở Việt Nam thì sẽ được điều hướng tới resouce đặt tại Singapore(Nếu ở đấy có độ trễ thấp nhất.)
- Có Health check(để thực hiện chuyển đổi dự phòng)
![[00 Meta/01 Attachments/Pasted image 20230311235240.png]]

### 🍃 Failover
- Tự động chuyển đổi dự phòng tới các instance healthy nếu primary instance được đánh giá là unhealthy.
![[00 Meta/01 Attachments/Pasted image 20230312002759.png]]

### 🍃 Geolocation
- Khác với **Latency**(ở gần chưa chắc đã có độ trễ thấp nhất).
- **Dựa vào vị trí của user để định tuyến**.
- Nên tạo một **default** record(sẽ được sử dụng trong trường hợp không tìm được vị trí phù hợp)
- Usage: web định vị(kiểu baemin, ở đâu thì xác định vị trí gần để giao hàng cho nóng), giới hạn phân phối nội dung tới từng khu vực, load balancer, ...
- Có thể kết hợp với Health Check

### 🍃 Geoproximity Route
![[00 Meta/01 Attachments/Pasted image 20230312004415.png]]

- Vẫn dựa vào vị trí của user và resouce, nhưng thằng này có khả năng điều chỉnh lượng traffic tới resouce bằng thông só bias. Set **bias** càng cao thì tỉ lệ traffic đổ về càng lớn.

### 🍃 Multi-value
- Dùng khi muốn định tuyến traffic tới nhiều resources.
- Có thể kết hợp với Health Checks( sẽ chỉ trả về các values/resources healthy)
- Tối đa trả về 8 values healthy cho từng query.
- **Multi-Value không thay thế cho một ELB**.
- Nó khác với **Simple**, vì nó có health checks, **Simple** trả về nhiều values nhưng có thể trong đó có unhealthy value.

## 🌿 Health Check
- HTTP Health Check chỉ sử dụng để check cho các public resources.
- Health Check => Tự động chuyển đổi dự phòng nếu phát hiện ra unhealth resource.
- Health Check được kết hợp với CW(CloudWatch) metrics.
- Có 3 kiểu health check:

### 🍃 **Monitor on endpoint**
- Có khoảng 15 health checkers sẽ check health endpoint
	- Ngưỡng health/unhealthy mặc định = 3
	- 30s gọi check một lần ( có thể set xuống 10s nhưng phí đắt hơn)
	- Hỗ trợ giao thức: HTTP, HTTPS và TCP
	- Nếu > 18% health checkers báo cáo là healthy thì Route 53 sẽ đánh giá nó là healthy và ngược lại.
- Chỉ check pass với các responses có code là 2XX và 3XX
- Có thể đánh giá Health dựa trên 5120 bytes đầu tiên của response.
- Phải config route/firewall cho phép nhận requests từ Route 53 để Health Check.
### 🍃 **Calculated health checks**
- Kết hợp kết quả của nhiều health check con cho một healthcheck cha, để đánh giá tình trạng sức khỏe của resource.
- Có thể sử dụng **AND, OR, NOT**
- Có thể set max 256 health check con.
- Chỉ định số lượng health check con pass là bao nhiêu để health check cha pass.
- Usage: thực hiện bảo trì.
### 🍃 **Private Hosted Zones**
- Route 53 thực hiện health check từ bên ngoài VPC.
- Do không thể truy cập trực tiếp tới các **private endpoints**, nên cần phải tạo CloudWatch và Route 53 đọc metrics của CW để đánh giá trình trạng sức khỏe của resources.
![[00 Meta/01 Attachments/Pasted image 20230312001849.png]]

## 🌿 Domain Registar & DNS Service
- Bạn có thể mua hoặc đăng ký tên miền ở chỗ khác và sử dụng DNS Service ở chỗ khác để quản lý.
![[00 Meta/01 Attachments/Pasted image 20230312010504.png]]

1. Tạo Hosted Zone trên Route 53
2. Update NS record ở bên thứ 3(vd GoDaddy) sử dụng **Route 53 Name Server**.

- **Domain Registar != DNS Service**

