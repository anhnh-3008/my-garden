---
title: 🌱 AWS Lambda - ver2
tags:
  - aws
date: 2023-03-28
---

## 🌿 Limits
- Giới hạn của Lambda trên **từng region"
	- **Excution:**
		- Bộ nhớ được cấp phát: 128MB - 10GB
		- Thời gian excution: 900 senconds(15 phút)
		- Các biến môi trường: 4KB
		- Dung lượng lưu trữ trong "funtion container"(in/tmp): 512MB - 10GB
		- Thực thi đồng thời: 1000(có thể gia tăng)
	- **Deployment:**
		- Lambda function deployment size(compresed .zip): 50MB
		- Size of uncompressed deployment(code + dependencied): 250MB
		- Có thể sử dụng thư mục /tmp để load các files khác để khởi động.
		- Các biến môi trường: 4KB

- Trong bài thi nếu người ta hỏi cần 30GB of RAM hay 30 phút excution times hay cần load các files lớn mấy GB thì => không phải Lambda đâu.

## 🌿 Networking
- Mặc định Lambda function được launch bên ngoài VPC của chúng ta, nó chạy trong một VPC của AWS. Vì vậy mà nó không thể truy cập được tới các tài nguyên trong VPC của chúng ta(RDS, ElastiCache, internal ELB, ...)
![[00 Meta/01 Attachments/Pasted image 20230328164920.png]]

- Để giải quyết vấn đề này, chúng ta cần launch Lambda Funtion trong VPC. 
	- Đầu tiên cần xác định VPC ID, Subnets và Security Groups.
	- Lambda sẽ tạo ra một ENI trong subnets, thông qua đó để giao tiếp với các resources nằm trong VPC.
![[00 Meta/01 Attachments/Pasted image 20230328165321.png]]

- Trường hợp sử dụng phổ biến nhất mà cần Lambda nằm trong VPC đó là connect với RDS Proxy.
- Thật ra để Lambda connect trực tiếp với RDS thì cũng được, chỉ cần public access là được. Nhưng vấn đề là không được để Lambda connect trực tiếp với RDS vì rất có thể nó sẽ mở thêm quá nhiều các kết nối, vượt quá khả năng chịu tải của RDS.
- Giải pháp là sử dụng thằng RDS Proxy ở giữa để nó điều hoà nội tiết các kết nối. **Lý do phải cho thằng Lambda này vào VPC bởi vì RDS Proxy không thể set truy cập public được**.
![[00 Meta/01 Attachments/Pasted image 20230328172457.png]]