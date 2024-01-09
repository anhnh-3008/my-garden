---
title: "🌱 High Performance Computing in AWS"
tags: [aws]
date: 2023-04-24
alias: [hpc]
---

## 🌿 What is HPC - High Perfomance Computing?
- Là thuật ngữ để chỉ các hệ thống yêu cầu khả năng tính toán cao.
	- vd như các hệ thống dự báo thời tiết, machine learning, deep learning, mô hình hoá rủi ro tài chính, ...
- Và cloud là một môi trường vô cùng thuận lợi cho việc phát triển các hệ thống HPC.
	- Chúng ta có thể tạo rất nhiều resource trên cloud.
	- Nhanh chóng áp dụng, mở rộng theo nhu cầu của hệ thống.
	- Đầy đủ services để hỗ trợ cho việc phát triển, mối lo duy nhất chỉ là tài chính thôi =))

Vậy, AWS cung cấp những dịch vụ nào để hỗ trợ phát triển dự án HPC?

## 🌿 Data Management & Transfer
- **AWS Direct Connect** - Có thể chuyển GB/s data lên Cloud, thông qua một private secure network.
- **Snowball & Snowmobile** - Có thể chuyển PB data lên cloud, sử dụng các thiết bị lưu trữ vật lý, dump dữ liệu và chuyển về datacenter để migrate.
- **AWS DataSync** - Đồng bộ dữ liệu lớn giữa on-premise và các dịch vụ lưu trữ trên cloud. 

## 🌿 Computing & Networking
- **EC2 Instances**
	- Tối ưu CPU, GPU.
	- Có thể lựa chọn các options thuê dịch vụ là Spot Instances / Spot Fleets để tiết kiệm giá cũng như thực hiện tự động mở rộng hệ thống.
	- EC2 Placemenet: lựa chọn chiến lược đặt vị trí của các EC2 Instances phù hợp với yêu cầu của hệ thống.
- **EC2 Enhanced Networking(SR-IOV)**
	- Băng thông cao hơn, PPS(packet per second) cao hơn, độ trễ thấp hơn.
	- Option1: sử dụng **ENA - Elastic Network Adapter** có thể hỗ trợ băng thông tối đa là 100Gbs
	- Option2: Intel 82599 VF hỗ trợ tối đa là 10GBs
- **Elastic Fabric Adapter - EFA**
	- Phiên bản cải tiến của ENA để hỗ trợ cho hệ thống HPC, chỉ hỗ trợ với hệ điều hành **Linux**.
	- Hỗ trợ khả năng giao tiếp tuyệt vời giữa các node của hệ thống, phù hợp với các hệ thống yêu cầu khả năng tính toán kết hợp giữa nhiều Instances.
	- Tận dụng Message Passing Interface tiêu chuẩn.

## 🌿 Storage
- Instance Storage
	- **EBS**
	- **Instance Storage**
- Network Storage
	- **S3**
	- **EFS**
	- **Amazon FSx for Lustre**

## 🌿 Automation & Orchetration
- **AWS Batch**
	- Hỗ trợ đồng thời chạy các jobs.
	- Dễ dàng lập lịch
- **AWS ParallelCluster**
	- Một tool quản lý dùng để delpoy HPC lên AWS.
	- Thiết lập sử dụng text files.
		- Tự động tạo VPC, Subnets, cluster type hoặc instance type.
		- **Có khả năng bật EFA trên các cluster.**