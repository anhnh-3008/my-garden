---
title: "🌱 Amazon EKS - Elastic Kubernetes Service"
tags: [aws]
date: 2023-03-27
alias: [eks]
---

## 🌿 What?
- Là một cách để launch containers được quản lý bởi các **Kubernetes clusters trên AWS.**
- Kubernetes là một hệ thống open-source hỗ trợ việc tự động deployment, scaling và quản lý các app chạy trên containers.
- Cái này là một lựa chọn khác, bên cạnh ECS, cùng chung mục đích những khác API.
- EKS hỗ trợ **EC2** nếu chúng ta muốn triển khai các worker nodes hoặc **Fargate** nếu chúng ta muốn triển khai các serverless containers.
- **Use Cases:** Nếu công ty, tổ chức đã áp dụng Kubernetes vào hệ thống, thì sài cái này thôi.
- **Kubernetes là dịch vụ riêng, không thuộc bất kỳ cloud nào, vì vậy chúng ta có thể sử dụng Kubernetes ở các Cloud khác nữa. Có thể chọn EKS để phòng cho sau này muốn chuyển qua sử dụng một Cloud khác.**
## 🌿 Node Types
- **Managed Node Groups**
	- Tạo và quản lý Nodes(EC2 Instances) cho chúng ta.
	- Nodes là một phần của ASG đươc quản lý bởi AWS.
	- Hỗ trợ On-demand và Spot Instances
- **Self-Managed Nodes**
	- Chúng ta tự tạo các nodes và đăng ký chúng với EKS clusters và được quản lý bởi một ASG.
	- Hỗ trợ On-demand và Spot Instances
- **AWS Fargate**
	- Không yêu cầu bảo trì, không cần quản lý nodes.

## 🌿 Data Volume
- Cần chỉ định một **StorageClass** rõ ràng cho EKS cluster.
- Hỗ trợ với:
	- Amazon EBS
	- Amazon EFS(dùng được với Fargate)
	- Amazon FSx for Lustre
	- Amazon FSx for NetApp ONTAP
