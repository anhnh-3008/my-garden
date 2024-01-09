---
title: "🌱 EBS Volume - Elastic Block Store"
tags: [aws]
date: 2023-03-03
alias: [EBS, EBS Volume]
---

## 🌿 What?
![[00 Meta/01 Attachments/Screenshot 2023-03-03 at 11.24.50.png]]
- Là một dịch vụ lưu trữ thông qua các **virtual disks**, giúp chúng ta có thể truy xuất dữ liệu từ các EC2 Instances (a network drive, not a physical drive).
	- EBS sẽ sử dụng network để giao tiếp với các EC2 Instance, vì vậy có thể có chút độ trễ.
- Cho phép lưu trữ dữ liệu cả khi đã terminate EC2 instance. Có thể mount lại dữ liệu nếu cần.
- 1 EBS chỉ mounted được tới 1 instance tại cùng một thời điểm.
	- Có thể detached khỏi một Instance và attached vào một Instance khác dễ dàng và nhanh chóng.
- Bound trong 1 AZ chỉ định, không sử dụng được cho các EC2 instance ở khác AZ.
	- Để move một volume qua AZ khác, chúng ta cần snapshot nó.
- Có thể hiểu nó như một cái USB, có thể mang đi cắm vào các EC2 instances khác cần sử dụng dữ liệu.
- Đương nhiên chúng ta sẽ cần chỉ định cấu hình(bao nhiêu Gbs và IOPS - Input/output Operations Per Second - tốc độ đọc ghi thế nào)
	- Có thể thêm tiền để upgrade cấu hình.

## 🌿 EBS Snapshots
![[00 Meta/01 Attachments/Screenshot 2023-03-03 at 11.56.30.png]]
- Là tính năng giúp cta sao chép EBS Volume, bao gồm dữ liệu, tệp tin và cấu hình của chúng.
- Giúp move volume giữa những AZs khác nhau.

### 🍃 Features

1. 🌱 EBS Snapshot Archive
	- Có thể chuyển Snapshot vào một **archive tier** thay vì lưu trữ thông thường, cách này rẻ hơn 75%.
	- Mất 24-72h để restoring lại.

2. 🌱 Recycle Bin for EBS Snapshots
	- Giữ lại những snapshots đã bị xóa, từ đó có thể lấy lại được nếu chẳng may chúng ta xóa nhầm.
	- Chỉ định thời gian giữ lại (1 ngày - 1 năm)

3. 🌱 Fast Snapshot Restore (FSR)
	- Cho phép khởi tạo không có độ trễ cho lần đầu tiên. Nếu cta có snapshot lớn và muốn khởi tạo EBS Volume nhanh.
	- Tính năng này cần trả thêm phí để sử dụng.

## 🌿 EBS Volume Types
-   Có 6 loại:
	- gp2/gp3(SSD): cho những nhu cầu sử dụng tiêu chuẩn, cân bằng giữa giá cả và hiệu suất sử dụng. Phù hợp với nhiều ứng dụng.
	- io1/io2(SSD): hiệu suất tốt nhất, sử dụng cho những ứng dụng cần thực hiện tính toán tốc độ cao, I/O tốt.
	- st1(HDD): Giá thấp hơn, sử dụng HDD phục vụ lưu trữ dữ liệu thường xuyên truy xuất và yêu cầu khả năng truyền tải dữ liệu lớn.
	- sc1(HDD): Giá thấp nhất, để lưu trữ dữ liệu lớn và dữ liệu không được thường xuyên truy xuất.
- Các đặc điểm của EBS Volume là: Size, Throughput, IOPS(I/O Operating Per Second)
- Chỉ gp2/gp3 và io I/io2 mới có thể sử dụng để làm boot volumes. 

### 🍃 General Purpose SSD
- Giá cả hợp lý, độ trễ thấp.
- Sử dụng làm boot volumes, virtual desktops, development and test environments.
- 1Gb - 16Tb
|gp3|gp2|
|----|----|
|Baseline là 3000 IOPS và throughput of 125 Mib/s|Chỉ lên được 3000 IOPS là max|
|IOPS và Throughput có thể set độc lập|IOPS và Throughput luôn linked với nhau|

### 🍃 Provisioned IOPS
- Dự án có nghiệp vụ quan trọng cần duy trì hiệu suất IOPS hoặc rõ hơn là cần nhiều hơn 16000 IOPS.
- Là lựa chọn tuyệt vời cho **database workloads**
- 4Gb - 16Tb
	- Max: 64000 IOPS với **Nitro EC2 instance** và 32000 với những EC2 instances thường.
	- Giống gp3, có thể nâng IOPS độc lập.
	- io2 có độ bền cao hơn và IOPS trên GiB cao hơn io1 với cùng mức giá.
- io2 Block Express (4GB - 64 TB)
	- Độ trễ cực thấp.
	- Max: 256000 IOPS
- Hỗ trợ Multi-attach
	- Cho phép một EBS Volume attach với nhiều EC2 Instances trong cùng một AZ.
	- Mỗi Instance đều có full quyền đọc ghi.
	- Max có thể attach được 16 Instances một lúc.

### 🍃 Hard Disk Drivers
- Không thể là một boot volume
- 125GB - 16TB
- Throughput Optimized HDD - st1
	- Use cases: Big Data, Data Warehouses
	- Max Throughput: 500 MiB/s - max IOPS 500
- Cold HDD - sc1
	- Dùng để lưu trữ data không thường xuyên truy xuất
	- Chi phí thấp nhất
	- Max throughput 250MiB/s - max IOPS 250

## 🌿 EBS Encryption
- Mã hóa dữ liệu trước khi được lưu trữ.
- Sau khi tạo một EBS Volume được mã hóa:
	- Toàn bộ data trong volume đều được mã hóa
	- Toàn bộ dữ liệu chuyển đổi giữa instance và volume đều được mã hóa
	- Tất cả snapshots đều được mã hóa.
	- Tạo volume mới phải tạo từ snapshot.
- Cơ chế mã hóa và giải mã được thực hiện tự động.
- Quá trình mã hóa không ảnh hưởng nhiều đến độ trễ.
- Được mã hóa bởi thuật toán AES-256.
- Nếu tạo một EBS volume không mã hóa, muốn chuyển qua một EBS volume mã hóa:
	- Tạo snapchat từ Volume đang sử dụng.
	- Tạo một Volume từ snapchat -> chọn encrypt.
	- Attach tới EC2 Instance.
