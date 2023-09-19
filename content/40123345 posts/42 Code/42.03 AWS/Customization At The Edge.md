---
title: "🌱 Customization At The Edge"
tags: [aws]
date: 2023-03-28
alias: [edge function]
---

## 🌿 What?
- Trong thực tế, có những lúc app của chúng ta cần chạy một số form logic trên các edges. Để thực hiện việc này chúng ta có thể sử dụng **Edge Function.**
- **Edge Function:**
	- Thực thi một đoạn code của chúng ta trên các bản phân phối của CloudFront.
	- Các đoạn code được chạy ở gần với users, đạt được độ trễ tối đa.
- CloudFront cung cấp 2 loại: **CloudFront Functions & Lambda@Edge**
- Chúng ta không cần tạo, quản lý hay triển khai bất kỳ server, **serverless.**

- Use Cases: khi muốn custom lại CDN content.
- Chỉ phải trả tiền khi sử dụng, còn để đấy không động vào thì không mất phí.

## 🌿 CloudFront Functions
- Là các lightweight functions được viết bởi Javascript.
- Có khả năng mở rộng cao, độ trễ thấp
- Thời gian khởi động cực nhanh, tốc độ xử lý requests là cả **triệu requests/giây.**
- Sử dụng để thực hiện thay đổi requests/responses của user.
- Đây là tính năng có sẵn của CloudFront(code được quản lý toàn bộ trong CloudFront)
![[00 Meta/01 Attachments/Pasted image 20230328163241.png]]

- Use cases:
	- Cache key
	- Thao tác với Header(thêm, xoá, sửa HTTP headers trong các requests hoặc responses)
	- Viết lại URL hoặc thực hiện redirects.
	- Request xác thực hoặc phân quyền.

## 🌿 Lambda@Edge
- Lambda functions được viết bởi NodeJS hoặc Python.
- Scales lên 1000 yêu cầu/giây
- Sử dụng để thay đổi các requests/response của cả viewer và origin server.
- Cấp quyền cho các funtions trong một AWS Region, sau đó CloudFront sẽ sao chép đến các locations của nó.
![[00 Meta/01 Attachments/Pasted image 20230328163706.png]]
- Use cases:
	- Các tác vụ cần thời gian lâu hơn để thực thi.
	- Điều chỉnh CPU hoặc memory
	- Code của chúng ta phụ thuộc vào một thư viện bên thứ 3.
	- Network access để sử dụng các services nội bộ.
	- Truy cập vào hệ thống file hoặc body của các HTTP requests -> tuỳ chỉnh được nhiều hơn.