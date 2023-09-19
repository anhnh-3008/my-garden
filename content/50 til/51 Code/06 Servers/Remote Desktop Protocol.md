---
title: "🌱 Remote Desktop Protocol"
tags: [til, server]
date: 2022-10-17
---

Bình thường các server mình được làm trước đây đều là Ubuntu Server, muốn truy cập lên thì dùng ssh-key là được. Nhưng do spec của dự án hiện tại mình làm có yêu cầu sử dụng Window Server. Khi gửi thông tin Server(IP, users, pass) anh PSM có gợi ý dùng `RDP Client` để truy cập vào. Cơ mà `RDP Client` là cái khỉ gì 😅

## 🌿 What?
- 🌱`RDP` là một giao thức độc quyền được phát triển bởi Microsoft, cung cấp cho người dùng giao diện để truy cập đến một máy tính khác thông qua kết nối internet. Bạn có thể làm mọi thứ với PC remote như một PC vật lý bình thường. Ví dụ như:  
	- Sử dụng các ứng dụng của PC remote.
	- Truy cập file và các tài nguyên mạng của PC remote.
	- Tắt các ứng dụng khi bạn thoát khỏi `RDP Client` (giống shut down PC vật lý.)
- 🌱 `Remote Desktop Protocol severs` được dùng để các clients kết nối, severs mặc định của RDP là `TCP port 3389` và `UDP port 3389`.
- 🌱 **Remote Desktop Connection** được tích hợp cho `RDP Clients` trong hệ điều hành Windows.

## 🌿 Quick connect to a Windows Server from Ubuntu using RDP Client

- 1️⃣ Step 1: Đảm bảo PC hoặc server Windows mà bạn muốn truy cập đã được bật Remote Desktop Connections. 
- 🌱 Nếu chưa bạn có thể xem cách bật ở [đây](https://www.digitalcitizen.life/enable-remote-desktop-windows/).
- 2️⃣ Step 2: Mặc định Ubuntu cung cấp `Remmina` để hỗ trợ RDP. Turn on!

![[00 Meta/01 Attachments/01.02 TIL/Server/Remote Desktop Protocol/Pasted image 20221017142240.png]]

- 3️⃣ Step 3: Tạo một connect mới.

![[00 Meta/01 Attachments/01.02 TIL/Server/Remote Desktop Protocol/Pasted image 20221017171736.png]]

- 4️⃣ Step 4: Điền thông tin server.
	- Tiếp theo là setting độ phân giải và color depth của màn hình desktop remote. Mặc định sẽ chọn độ phân giải và color depth ở mức cao nhất. Tuy nhiên, setting 2 thông số này thấp hơn sẽ cải thiện khá nhiều perfomance đấy.
	- Nếu muốn chia sẻ folder với Windows Server, check folder box và chỉ định folder cần chia sẻ.
	- Ngoài ra ở mục Advanced, bạn có thể bật/tắt tiếng, chia sẻ máy in, tắt đồng bộ cho bộ nhớ tạm, ...

![[00 Meta/01 Attachments/01.02 TIL/Server/Remote Desktop Protocol/Pasted image 20221017172232.png]]

- 5️⃣ Step 5: Lưu và chạy thôi!

![[00 Meta/01 Attachments/01.02 TIL/Server/Remote Desktop Protocol/Pasted image 20221017174839.png]]


## 🌿 Góc so sánh

- 🌱 Theo định nghĩa, công dụng của thằng này nghe cũng khá giống TeamView nhỉ 😀 So sánh thôi 😗

Remote Desktop Protocol | TeamView
------------ | ------------
Là giao thức được tích hợp sẵn trong hệ điều hành Windows và được phát triển độc quyền bởi công ty Microsoft  | Là một phần mềm chia sẻ quyền điều hành máy tính được phát triển bởi TeamViewer GmbH
Không cho phép người dùng theo dõi tác vụ trên máy remote | Cho phép người dùng dõi tác vụ trên máy remote
Yêu cầu cấu hình port chuyển tiếp trên `firewall` hoặc route của máy remote | Chỉ cần cài đặt là dùng bình thường

- 🌱 Nhìn chung TeamView ngon và dễ sử dụng hơn RDP nhưng TeamView lại tiềm ẩn rủi ro bị lộ dữ liệu,  thông tin, như ở công ty mình TeamView được liệt vào danh sách đen không được cài đặt ấy.
- 🌱 Tùy theo bối cảnh mọi người có thể cân nhắc sử dụng giữa 2 này nhé. 

## 🌿 Tham khảo
- https://learn.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients
- https://www.techrepublic.com/article/teamviewer-vs-remote-desktop/