---
title: "🌱 NAT Gateway"
tags: [aws]
date: 2023-04-17
alias: [nat gateway, natgw]
---

## 🌿 What?
- Giống như  [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/NAT Instance|NAT Instance]], cũng có tác dụng để định tuyến traffic từ các EC2 Instances trong private subnet để kết nối internet, nhưng NAT Gateway sẽ được AWS hỗ trợ hết, mình chỉ cần dùng thôi.
- Vì do AWS bảo kê nên nó HA, có khả năng mở rộng theo nhu cầu sử dụng của các instances trong subnet, có thể tự động khởi động lại khi có lỗi.
- Không cần phải quản lý Security Group
- NATGW được tạo trên một AZ chỉ định, và được gán một ElasticIP.
- Bắt buộc phải kết hợp cùng với [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|IGW]].
![[00 Meta/01 Attachments/Pasted image 20230417214127.png]]
- Như đã biết thì trong Private Subnet không thể kết nối được với mạng internet, vì vậy cần phải sử dụng [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|route table]] để định tuyến traffic tới resource(ở đây là NATGW) bên public subnet để nó trigger tới Router,  Router như cái phễu đổ hết traffic vào [[40123345 posts/42 Code/42.03 AWS/Networking - VPC/IGW - Internet Gateway & Route Tables|IGW]] để gửi lên internet. 
