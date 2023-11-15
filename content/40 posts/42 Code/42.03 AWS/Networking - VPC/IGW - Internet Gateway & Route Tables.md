---
title: "🌱 IGW - Internet Gateway & Route Tables"
tags: [aws]
date: 2023-04-16
alias: [internet gateway, igw, route table]
---

## 🌿 What?
- Là dịch vụ cho phép các resources(vd như EC2) trong một [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]] có thể kết nối được với internet.
- HA, mở rộng chiều ngang theo nhu cầu sử dụng.
- Phải được tạo riêng biệt với một [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]].
- Một [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]] chỉ có thể connect với một IGW và ngược lại.
- Và route tables cũng phải được chỉnh sửa.
![[00 Meta/01 Attachments/Pasted image 20230416210334.png]]
- Kịch bản là EC2 Instance sẽ dựa vào Route Table để connect tới Router, Router sẽ điều hướng requests qua Internet Gateway, từ đây sẽ thực hiện kết nối với internet.
