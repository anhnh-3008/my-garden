---
title: "🌱 Solution Architect Discussion - theclothes.com"
tags: [aws, architecture]
date: 2023-03-12
---

## 🌿 Đề bài
- Một web bán quần áo, cho phép người dùng mua bán quần áo online.
- Website có cả trăm người dùng truy cập một lúc.
- Cần scale, và luôn giữ trạng thái sử dụng của toàn bộ người dùng.
- Cần lưu thông tin cá nhân của người dùng vào database.

## 🌿 Kiến trúc áp dụng
![[00 Meta/01 Attachments/Pasted image 20230312223816.png]]
- Áp dụng kiến trúc cũ của web **whattimeisit.com**.
- Muốn giữ trạng thái của người dùng, ý tưởng đầu tiên là cần định tuyến đến đúng instance đã truy cập trước đó -> Có thể bật Stick Session cho con ELB. Tuy nhiên cách này sẽ làm mất độ cân bằng tài do có thể có quá nhiều users cùng stick trên một instance.
- Đổi qua dùng kiểu lưu trạng thái mua hàng của user vào cookie và lưu dưới trình duyệt của user. Tuy nhiên cookie dễ bị thay đổi, thêm nữa chỉ có thể lưu trong 4Kb, quá ít, chả lưu được gì.
- Đến tầm này thì thuê luôn một con **ElastiCache** dùng cho nó máu. Chúng ta sẽ lưu thông tin mua bán hàng của user tại đây. Ở bên phía user sẽ lưu một session_id, khi truy cập vào bất kì instance nào, chỉ cần mã session_id là hợp lệ, hệ thống sẽ tìm trong **ElasticCache** để trả về thông tin cho user.
- Trong trường hợp session_id không hợp lệ hoặc cache lâu quá hết hạn bị xóa đi, hệ thống sẽ tìm trong **RDS - Relational Database System** để lấy thông tin, lưu lại vào trong **ElasticCache** để dùng lại cho những lần sau.
- Về vấn đề, cùng một thời điểm có cả trăm người dùng truy cập vào trang web, chúng ta sẽ scale read cho **RDS** để thực hiện đọc dữ liệu nhanh hơn.
- Phòng tránh thiên tai, bật Multi-AZ cho ELB, ElastiCache, RDS, đặt EC2 Instance ở nhiều AZs.
- Cuối cùng là cần tạo đầy đủ các rules cho **Security Group** của từng phần một.
	- ELB - Nhận HTTP/HTTPS từ 0.0.0.0(every requests)
	- EC2 Instance - Chỉ nhận requests từ ELB
	- ElastiCache - Chỉ nhận requests từ EC2 Instances
	- RDS - Chỉ nhận requests từ EC2 Instances
- ElastiCache:
	- Lưu session
	- Lưu dữ liệu cần sử dụng lại từ RDS
	- Bật Multi-AZ
- RDS:
	- Lưu thông tin của người dùng
	- Scale read để cải thiện tốc độ đọc của website
	- Bật Multi-AZ để tránh thảm họa.
