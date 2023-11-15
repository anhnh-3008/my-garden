---
title: "🌱 Bastion Host"
tags: [aws]
date: 2023-04-16
alias: [bastion]
---

## 🌿 What?
- Vì tất cả các EC2 Instances của chúng ta đều nằm trong [[40 posts/42 Code/42.03 AWS/Networking - VPC/VPC - Virtual Private Cloud|VPC]], chính vì vậy không thể để người dùng trực tiếp từ bên ngoài truy cập vào được, sẽ có nhiều rủi ro về bảo mật.
- Để giảm thiểu rủi ro, chúng ta sẽ tạo một Bastion Host trong một EC2 Instance, nó sẽ là một pháo đài dựng trước các EC2 server của chúng ta.
- Con Bastion đặt public để người dùng SSH vào, sau SSH vào xong, người dùng sẽ tiếp tục từ đây SSH tiếp vào các EC2 Server.
- Để tăng thêm tính bảo mật, có thể restrict subnet IP từ con Bastion luôn.
- Lưu ý là cần setup Security Group để các phần có thể giao tiếp được với nhau.
![[00 Meta/01 Attachments/Pasted image 20230416213349.png]]
