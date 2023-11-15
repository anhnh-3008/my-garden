---
title: "🌱 EC2 Hibernate"
tags: [aws]
date: 2023-03-02
---

## 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20230302224154.png]]
- Là một service giúp giữ lại trạng thái, toàn bộ bộ nhớ của một instance vào ổ đĩa EBS trước khi nó stop hoặc bị terminate.
- Giúp Instance khởi động nhanh hơn.
- Root EBS volume phải được mã hóa.
- Giúp tiết kiệm chi phí khi chúng ta có thể giải phóng tài nguyên khi không cần sử dụng và không sợ phải mất dữ liệu hoặc cấu hình của một instance.
- Use cases:
	- Những dự án có tiến trình khởi chạy lâu.
	- Muốn lưu trữ trạng thái của RAM.


## 🌿 Good to Know
- Hỗ trợ các Instance Families: C3, C4, C5, I3, M3, M4, R3, R4, R2, T3, ...
- Instance RAM size: phải nhỏ hơn 150Gb
- Root Volume: phải là EBS, được mã hóa. Không hỗ trợ với những Instances sử dụng **instance store** và volume lớn.
- Có sẵn với các purchasing options sau: On-Demand, Reserved và Spot Instances.
- Một instance không thể lưu trữ trạng thái quá 60 ngày(có thể thay đổi số này nhưng đây là thời gian tiêu chuẩn).