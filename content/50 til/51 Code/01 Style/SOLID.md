---
title: "💪 What is SOLID?"
tags: [til, style]
date: 2022-10-05
---

🌱 SOLID là cụm từ  tạo thành từ những chữ cái viết tắt của 5 nguyên tắc được đúc kết từ 'xương máu' của rất nhiều lập trình viên đi trước =)) Nếu đã từng làm dự án thực tế, mọi người sẽ đều biết là gần 80% thời gian sẽ là bảo trì hệ thống(thêm tính năng, sửa lỗi, ...). Áp dụng SOLID, công việc bảo trì  và mở rộng sẽ dễ dàng hơn rất nhiều. Các nguyên tắc này cũng ảnh hưởng nhiều bởi 4 nguyên lý cơ bản của lập trình hướng đối tượng(OOP). 

## 🌿 Single Responsibility Principle
- Mỗi class chỉ nên thực hiện **một nhiệm vụ** đơn lẻ!

![[00 Meta/01 Attachments/Single Responsibility Principle.png]]


## 🌿 Open/Closed Principle
- Khi thêm tính năng cho class, nên viết những class mới kế thừa class cần mở rộng.
- 

![[00 Meta/01 Attachments/Open-Closed Principle.png]]

## 🌿 Liskov Substitution Principle
- Các đối tượng của lớp con nên có thể thay thế cho các đối tượng của lớp cha mà không làm thay đổi tính đúng đắn của chương trình.


![[00 Meta/01 Attachments/Liskov Subtitution Principle.png]]

## 🌿 Interface Segregation Principle
- Nên tạo ra các interface cụ thể thay vì một interface tổng quát.

![[00 Meta/01 Attachments/Interface Segregation Principle.png]]


## 🌿 Dependency Inversion Principle
- Các module cấp cao không nên phụ thuộc vào các module cấp thấp, cả hai nên phụ thuộc vào abstraction

![[00 Meta/01 Attachments/Dependency Inversion Principle.png]]