---
title: 🌱 Adapter
tags:
  - til
  - design-patterns
date: 2023-11-13
aliases: 
draft: false
---
# 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20231113132013.png]]

> [!note] Định nghĩa
> 
> **Adapter** is a structural design pattern that allows objects with incompatible interfaces to collaborate.

Adapter cung cấp khả năng linh hoạt cho objects, có thể sử dụng được theo nhiều định dạng.

Chắc mọi người đã từng nghe đến adapter cho MacBook.![[00 Meta/01 Attachments/Pasted image 20231113132520.png]]
Do MacBook chỉ hỗ trợ cổng typeC nhưng thực tế sử dụng chúng ta cần kết nối nhiều định dạng cổng khác nhau. Adapter là công cụ giúp chúng ta thực hiện được việc đó.

# 🚧 Problem

Giả sử chúng ta đang phát triển một app liên quan đến tài chính. Lúc đầu chúng ta call dữ liệu từ bên cung cấp dữ liệu chứng khoán với định dạng là XML và sử dụng định dạng XML để xử lý trong hệ thống luôn. Sau một thời gian, hệ thống nâng cấp khả năng phân tích dữ liệu bằng việc tích hợp với một bên thứ 3, nhưng vấn đề là bên thứ 3 chỉ nhận định dạng JSON thôi.

# 🛠️ Solution

Giải pháp chính là tạo một Adapter để chuyển đổi định dạng từ XML -> JSON.
![[00 Meta/01 Attachments/Pasted image 20231113133907.png]]

# 🌿 Class Adapter

Sử dụng Adapter khi chúng ta muốn giữ nguyên code cũ và thêm một class chuyển đổi để đáp ứng điều kiện của service mới.

![[00 Meta/01 Attachments/Pasted image 20231113132837.png]]


# 🌿 Refer 
- https://refactoring.guru/design-patterns/adapter