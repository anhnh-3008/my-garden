---
title: ♻️ Why is Redis so Fast
tags:
  - til
  - redis
date: 2022-10-05
---

🌱 Có 3 lý do chính giải thích điều này:

![[00 Meta/01 Attachments/3 Reasons why Redis is fast.png]]

- Redis là một cơ sở dữ liệu lưu trữ trên RAM. Tốc độ truy cập RAM đểu nhất cx nhanh hơn 1000 lần so với tốc độ truy cập ổ cứng. Mọi người có thể xem thêm 
- Redis sử dụng `IO multiplexing` và `single-threaded`. IO multiplexing là cơ chế đọc/ghi liên tục của RAM. RAM nhận tất cả các yêu cầu đọc/ghi dữ liệu, để vào một chỗ, sau đó dùng single-threaded lặp qua từng event để tiếp tục xử lý.
- Redis sử dụng một vài cấu trúc dữ liệu `lower-level`(String lưu thành SDS, ...).


## 🌿 Câu hỏi
- 🌱 Tại sao truy cập từ RAM lại nhanh hơn từ HDD?
[[50 til/51 Code/08 System Design/Why is RAM access faster than hard disk drive]]


P/s: Memcached cũng là một giải pháp khá phổ biến để giải quyết vấn đề cached dữ liệu, mọi người có thể tìm hiểu thêm nhé.

## 🌿  Tham khảo
- Free System Design - ByteByteGo - Trang 76