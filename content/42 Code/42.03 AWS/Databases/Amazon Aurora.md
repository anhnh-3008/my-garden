---
title: "🌱 Amazon Aurora"
tags: [aws]
date: 2023-03-08
alias: [aurora]
---

## 🌿 What?
- Là công nghệ độc quyền của AWS(không phải open source)
- Tương thích với Postgres và MySQL.
- Aurora là **AWS  cloud optimized**, x5 performance so với MySQL trên RDS và x3 performance so với Postgres trên RDS.
- Tự động tăng bộ nhớ, từ 10Gb(mặc định) có thể tăng lên 128TB
- Aurora có 15 replicas trong khi MySQL có 5, và replication process cũng nhanh hơn(10ms)
- Chuyển đổi dự phòng là tức thời. Đảm bảo High Available
- Gía của Aurora đắt hơn 20% so với RDS, nhưng nó cũng hiểu quả hơn.

## 🌿 High Availability và Read Scaling
- Luôn tạo ra 6 bản sao ở trên 3 AZ mỗi khi ghi gì đó vào DB. Có khả năng nhân rộng, tự hồi phục cũng như tự động mở rộng.
	- 4 bản sao trong 6 dùng để viết.
	- 3 bản sao dùng để đọc
- Có một Aurora Instance để ghi (master)
- Tự động chuyển đổi dự phòng nếu master có lỗi trong vòng chưa đến 30s.
- Master + 15 read replicas
- Hỗ trợ nhân rộng giữa các Region.

## 🌿 Aurora DB Cluster
![[00 Meta/01 Attachments/Pasted image 20230308141108.png]]

- Luôn chia sẻ dữ liệu lưu trữ với tất cả các cụm(master + read replicas)
- Client connect thẳng tới master để ghi dữ liệu(writer endpoint)
- Client conenct tới một Connection Load Balancing(reader endpoint) để truy cập đến cụm read replicas.

## 🌿 Feature of Aurora
- Tự động chuyển đổi dự phòng nếu có lỗi
- Liên tục backup và recovery
- Bảo mật và luôn sẵn sàng sử dụng
- Tự động scaling
- Zero downtime
- Có thể restore data tại bất kỳ thời điểm nào.

## 🌿 Custom EndPoint
- Cho phép xác định custom endpoint để thực hiện tác vụ riêng.
- Ví dụ cta có một cụm instance to hơn và nó tính toán tốt hơn, tạo một custom endpoint trỏ đến cụm đó để thực hiẹn các query phân tích dữ liệu(hay các query cần tính toán nhiều) để xử lý nhanh hơn.
![[00 Meta/01 Attachments/Pasted image 20230308144242.png]]

## 🌿 Aurora không có máy chủ
- Tự động tạo khởi tạo cũng như scaling dựa theo tình trạng sử dụng thực tế.
- Phù hợp với những ứng dụng không dự đoán trước được lưu lượng sử dụng.
- Không cần lên kế hoạch sử dụng.
- Dùng đến đâu trả đến đấy.

## 🌿 Aurora Multi-Master
- Trong trường hợp muốn chuyển đổi dự phòng ngay lập tức(chứ không phải đợi tầm khoảng 30s - HA), lựa chọn option này.
- Tất cả các nodes đều được dùng để R/W và liên kết trực tiếp với client.(thay vì chuyển node chỉ đọc lên làm master)
![[00 Meta/01 Attachments/Pasted image 20230308150206.png]]

## 🌿 Global Aurora
- **Aurora Cross Region Read replicas**
	- Đề phòng thảm hoạ
	- Dễ dàng đặt ở mọi nơi
- **Aurora Global Database (khuyên dùng)**
	- 1 Primary Region(đọc/ghi)
	- Tối đa 5 regions phụ(chỉ đọc), nhân bản có ping nhỏ hơn 1s
	- Mỗi region phụ có thể có tối đa 16 read replicas, giảm độ trễ khi đọc dữ liệu
	- Khôi phục dữ liệu sau thảm hoạ trong vòng 1 phút.
	- Chưa đến một giây để sao chép toàn bộ dữ liệu trên tất cả regions.

## 🌿 Aurora Machine Learning 
- Support services:
	- Amazon SageMaker(dùng với bất kỳ model ML nào)
	- Amazon Comprehend (dùng để phân tích cảm tính, đề xuất sản phẩm, ...)
![[00 Meta/01 Attachments/Pasted image 20230308152417.png]]

## 🌿 Aurora Backups
- Giống với RDS backups
	- Backup tự động
		- Lưu trữ trong 1-35 ngày
		- Backup tại tất cả các thời điểm, vì vậy chúng ta có thể lấy lại dữ liệu tại bất kỳ thời điểm nào.
	- Backup thủ công
		- User tự thực hiện
		- Lưu trữ vô thời hạn

## 🌿 Restore Options
- Restoring từ Aurora backup hoặc snapshot tạo một database mới.
- Restoring MySQL Aurora cluster từ S3
	- Tạo một backup sử dụng Percona XtraBackup
	- Lưu file backup vào S3
	- Restore từ file backup đó

## 🌿 Aurora Database Cloning
- Tạo một Database Cluster mới từ cái có sẵn.
- Nhanh hơn snapshot&restore
- Một DB mới được tạo ra, giống y hệt cái cũ nhưng không đồng bộ(ko liên quan gì đến nhau, vd một cái dùng cho staging, mọt cái dùng cho production)
- Rất nhanh và giá cả phải chăng
- Hữu ích khi muốn tạo một staging database từ production database và không ảnh hưởng đến môi trường production.