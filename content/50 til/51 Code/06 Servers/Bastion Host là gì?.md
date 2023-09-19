---
title: "🌱 Bastion Host là gì?"
tags: [til, server]
date: 2022-11-24
---

## 🌿 What?

![[00 Meta/01 Attachments/Pasted image 20221124184306.png]]

🌱 **Bastion Host(máy chủ pháo đài)** đúng như tên gọi, là một server sinh ra với sứ mệnh phòng vệ trước những mối hiểm họa có thể tấn công vào mạng lưới nội bộ của chúng ta.

🌱 **Theo định nghĩa của AWS**, **Bastion Host** là một server có mục đích cung cấp quyền truy cập vào mạng nội bộ từ mạng bên ngoài, chẳng hạn như Internet.

🌱 Hoạt động như cầu nối, đứng giữa **private instance** và những truy cập từ bên ngoài. Vì vậy khi tắt **Bastion**, người ngoài cũng sẽ không có cách nào có thể truy cập vào **private instance** của chúng ta.

## 🌿 Why?

🌱 Tăng khả năng bảo mật trong việc quản lý truy cập vào **private instance**.

## 🌿 Architect

![[00 Meta/01 Attachments/Pasted image 20221124183444.png]]

- **Bastion Host** đặt ở Public subnet, để bên ngoài truy cập vào được. 
- **Linux Instance** đặt ở Private subnet, chỉ có thể truy cập thông qua Bastion.

🌱 Về mặt lý thuyết, hành trình thật sự để từ ngoài có thể vào được Linux Instance đó là:
-   Internet Gateway
-   Route Table
-   Network ACL
-   Security Group
-   Bastion Host

## 🌿 Refer
📑 https://aws.amazon.com/blogs/security/how-to-record-ssh-sessions-established-through-a-bastion-host/