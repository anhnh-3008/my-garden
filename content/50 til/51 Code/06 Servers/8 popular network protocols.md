---
title: 🌱 8 popular network protocols
tags:
  - til
  - network
date: 2023-10-09
aliases: 
draft: false
---
- Network protocol là những phương thức chuẩn được dùng để trao đổi dữ liệu giữa nhiều máy tính với nhau trong 1 network.

![No alternative text description for this image](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_lossy/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F6f9e43fa-84d5-4875-817c-c2e1af75d16e_1280x1664.gif "No alternative text description for this image")
*Nguồn: ByteByteGo*

1. HTTP(Hyper Text Transform Protocol)
	- HTTP là một giao thức sử dụng để trao đổi các resources như là HTML docs. Giao thức này là nền tảng trao đổi dữ liệu giữa client-server, được ứng dụng trong phát triển Web.

2. HTTP/3
	- Là version tiếp theo của HTTP, chạy trên QUIC, một giao thức thiết kế cho các thiết bị mobile cần sử dụng dữ liệu nặng từ internet. Dựa trên UDP thay vì TCP, cho phép dữ liệu được hiển thị nhanh hơn. Ví dụ cho các thiết bị VR cần nhiều băng thông để load dữ liệu cho hình ảnh.

3. HTTPS
	- Là HTTP kết hợp thêm phương thức bảo mật mã hoá dữ liệu đầu cuối.

4. WebSocket
	- Là giao thức cung cấp khả năng truyền tải dữ liệu theo thời gian thực dựa trên TCP. Client và Server sau khi được kết nối sẽ liên tục push và pull dữ liệu của nhau để xử lý real-time. Các apps sử dụng giao thức này: app nhắn tin, trading, gaming, ...

5. TCP - Transmission Control Protocol
	- Là giao thức cung cấp khả năng chuyển đổi các gói dữ liệu thông qua internet.

6. UDP - User Datagram Protocol
	- UDP gửi trực tiếp các gói tin tới thiết bị mục tiêu, không cần phải xác định một kết nối trước đó. Giao thức thường được ứng dụng cho các trường hợp dữ liệu cần tương thích với thời điểm. Kiểu như voice chat, gọi điện,...

7. SMTP - Simple Mail Transfer Protocol 
	- Là giao thức sử dụng để gửi các thư điện tử thông qua internet.

8. FTP - File Transfer Protocol
	- Là giao thức dùng để trao đổi các file máy tính, vd như ảnh, .csv, .pdf, ... Download và Upload files.


Nguồn: ByteByteGo