---
title: "🌱 ASG - Auto Scaling Group"
tags: [aws]
date: 2023-03-07
alias: [asg]
---

## 🌿 What?
- Là một service của AWS hỗ trợ việc tự động mở rộng hay thu nhỏ số lượng instances để phù hợp với lượng tải của ứng dụng.
- Mục đích:
	- Thêm số lượng EC2 Instances để đáp ứng lượng tải tăng cao.
	- Giảm số lượng EC2 Instances để phù hợp với lượng tải ít đi.
	- Xác định được số lượng lớn nhất cũng như nhỏ nhất của các EC2 Instances.
	- Tự động đăng ký instances mới để cân bằng tải.
	- Tự động tạo lại một EC2 Instance thay thế trong trường hợp instance trước đó bị đánh giá là unhealthy.
- ASG are free (chỉ phải trả tiền thuê các EC2 instances)

## 🌿 Attributes
- Gọi là một **Launch Template**, bao gồm:
	- Nhưng thông tin về EC2 Instance:
		- AMI + Instance Type
		- EC2 User Data
		- EBS Volumes
		- Security Groups
		- SSH Key Pair
		- IAM Roles cho EC2 Instances
		- Network + Subnet
	- Thông tin Load Balancer
- Min Size/ Max Size/ Initial Capacity
- Scaling Policy
	- Khả năng auto scale dựa vào báo động CloudWatch - cái mà dùng để theo dõi metric(như Average CPU, ...) và từ đó có thể tính toán scale.

## 🌿 Scaling Policies
- Dynamic Scaling policies
	- Target Tracking Scaling
		- Đơn giản về dễ setup nhất
		- VD: tôi muốn trung bình ASG CPU ở khoảng 40%
	- Simple/Step Scaling
		- Scale dự theo thông tin của CloudWatch báo. Điều chỉnh mở rộng theo ngưỡng(min - max)
		- Vd nó báo CPU > 70% -> tự động add thêm 2 instances
		- vd nó bảo CPU < 30% -> tự động remove 1 instance
	- Scheduled Actions
		- Thực hiện mở rộng dựa theo lịch lên sẵn.
		- Ví dụ app dùng nhiều vào cuối tuần thì sẽ tăng instance lên vào thứ 7 và CN
	- Predictive Scaling
		- Dựa trên lịch sử khai thác dữ liệu của ứng dụng, ASG sẽ tự động điều chỉnh trước resources để luôn có để đáp ứng nhu cầu sử dụng.

## 🌿 Các chỉ số chính để đánh giá scale
- Chỉ số trung bình CPU của các instances
- Số requests trên từng Target
- Trung bình network in/out
- Any custom metric

## 🌿 Scaling cooldowns
- Sau mỗi hoạt động scale, ASG sẽ phải đợi **cooldown period( thời gian hồi chiêu )**, mặc định là 300s.
- Trong thời gian này, ASG sẽ không lauch hoặc terminate bất kỳ instance nào, việc này để đảm bảo các chỉ số được ổn định sau đó mới tiếp tục thực hiện các hoạt động scale khác.
- Sử dụng ready-to-use AMI để giảm thời gian config, từ đó giảm được quá trình hồi chiêu của ASG.