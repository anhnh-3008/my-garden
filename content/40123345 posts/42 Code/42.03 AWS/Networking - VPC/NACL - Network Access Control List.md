---
title: "🌱 Network Access Control List"
tags: [aws]
date: 2023-04-17
alias: [nacl]
---

## 🌿 What?
- Là tường lửa có nhiệm vụ kiểm soát traffic vào và ra của một subnet.
- Mỗi một subnet sẽ có một NACL riêng, khi tạo mới một subnet sẽ được gán với một NACL mặc định.
- Bạn cần phải xác định các rules cho NACL:
	- Mỗi rule sẽ được gắn với một số (từ 1-32766), số càng lớn càng có độ ưu tiên giảm dần.
	- Rule xuất hiện trước sẽ được ưu tiên áp dụng.
		- vd nếu define rule 100 Allow và rule 200 Deny, thì vẫn được Allow.
	- Qui tắc cuối cùng được đánh dấu hoa thị, nếu đến cái rule này thì reject hết, không nói nhiều.
	- AWS khuyến nghị chúng ta nên đặt rule tăng dần với step là 100.
- Những NACLs tạo mới tinh là nó sẽ reject tất cả. Còn với NACL mặc định. sẽ allow tất cả các traffic in/out.
- NACL là một lựa chọn phù hợp khi chúng ta muốn chặn địa chỉ IP tại tầng subnet.

## 🌿 Ephemeral Ports
- Cung cấp các cổng giao thức TCP hoặc UDP ngẫu nhiên để hình thành một kết nối mạng tạm thời giữa các ứng dụng hoặc các thiết bị trên internet.
- Clients sẽ connect tới một **defined port** và mong đợi rằng sẽ được nhận response từ một **ephemeral port**.
![[00 Meta/01 Attachments/Pasted image 20230417221409.png]]


