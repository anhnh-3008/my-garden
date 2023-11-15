---
title: "🌱 AWS System Manger"
tags: [aws]
date: 2023-04-27
alias: [ssm session manager]
---

## 🌿 SSM Session Manager
- Cho phép start một secure shell trên EC2 Instance hoặc on-premise server thông qua IAM Permissions, không cần thông qua [[40 posts/42 Code/42.03 AWS/Networking - VPC/Bastion Host|bastion host]], ssh.
- Không cần tạo cổng 22 luôn.
- Hỗ trợ cho Windows, Linux và MacOS.
- Dùng để send session log data đến [[40 posts/42 Code/42.03 AWS/S3|S3]] hoặc [[40 posts/42 Code/42.03 AWS/Monitoring/Amazon CloudWatch|CloudWatch]] Logs
![[00 Meta/01 Attachments/Pasted image 20230427153017.png]]

## 🌿 SSM Run Command
![[00 Meta/01 Attachments/Pasted image 20230427153727.png]]
- Thực thi script hoặc chạy một câu lệnh tới các EC2 Instances thông qua SSM Agent.
- Output sẽ có thể gửi tới [[40 posts/42 Code/42.03 AWS/Monitoring/Amazon CloudWatch|CloudWatch Logs]], [[40 posts/42 Code/42.03 AWS/S3|S3]], [[40 posts/42 Code/42.03 AWS/Amazon SNS - Simple Notification Service|SNS]].
- Có thể được gọi từ [[40 posts/42 Code/42.03 AWS/Monitoring/Amazon EventBridge|EventBridge]].

## 🌿 SSM Patch Manager
![[00 Meta/01 Attachments/Pasted image 20230427154104.png]]
- Tự động thực hiện các tiến trình update bản vá cho OS, hệ thống hoặc bảo mật.
- Hỗ trợ cho các EC2 Instances và on-premise servers.
- Hỗ trợ hệ điều hành Windows, Linux, MacOS.
- Patch on-demand hoặc lập lịch bằng **Maintenance Windows**.
- Scan Instance và gen ra báo cáo về những bản vá cần thiết(phát hiện thiếu bản vá nào).

## 🌿 Maintenance Windows
![[00 Meta/01 Attachments/Pasted image 20230427154512.png]]
- Giúp lập lịch để thực hiện các hành động theo maintain theo kế hoạch.
- Nó bao gồm:
	- Lịch.
	- DIễn ra trong bao lâu
	- Các Instances được chỉ định maintain
	- Các tasks được chỉ định thực thi

## 🌿 Automation
![[00 Meta/01 Attachments/Pasted image 20230427154703.png]]
- Giúp thực hiện một số các actions đơn giản và thường được sử dụng trong maintain và deploy.
	- vd như restart instance, create an AMI, [[40 posts/42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]] snapshot.
- **Automation Runbook** - Là nơi define các actions sẽ thực thi với các EC2 Instances hoặc AWS resources.
- Có thể trigger tới SSM Automation bằng các cách sau:
	- Thủ công kích hoạt thông qua AWS Console, SDK, CLI.
	- [[40 posts/42 Code/42.03 AWS/Monitoring/Amazon EventBridge|EventBridge]]
	- Maintenance Windows
	- [[40 posts/42 Code/42.03 AWS/Monitoring/AWS Config|AWS Config]]