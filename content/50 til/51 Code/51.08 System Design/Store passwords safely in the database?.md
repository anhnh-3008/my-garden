---
title: "🛡️ Store passwords safely in the database"
tags: [til, sys design, password]
date: 2022-10-04
draft: false
---

## Những điều không nên làm
---
- Không được lưu passwords dạng text trong db, vì bất cứ người nào có quyền connect vào db đều sẽ xem được nó.
- Lưu password hashes trực tiếp cũng không an toàn vì nó có thể vị vô hiệu hóa bởi những cuộc tấn công tính toán trước(`precomputation attacks`), vd như là `rainbow tables`.
- Để hạn chế `precomputation attacks`, chúng ta hãy `salt the passwords`.

### What is salt?
---
- Theo như hướng dẫn của OWASP, `salt` là một chuỗi duy nhất, được sinh ra ngẫu nhiên và được thêm cho từng password như là một phần của quá trình mã hóa.


## How to store?
---
![[00 Meta/01 Attachments/Pasted image 20221004102412.png]]
Theo hình trên, mọi người có thể hình dung các bước để lưu password vào DB như sau:
	1. User cung cấp password.
	2. Hệ thống sinh ra `salt` cho password.
	3. Trong DB sẽ lưu cả `salt` và `hash` được mã hóa từ `password + salt`. 

## How to validate?
---
**![](https://lh5.googleusercontent.com/VT3b8cvDZ6idbl8D3zYpTNiHhiBp72vR4CLfjAvJx0-Tjp7ZIGy63DtQeMfbtsjwfh5Q8uk3ch16YIMp4wCVwmzyb1A9-aTZ0cSFgyb3kVjvr9X3N_ZmP7-iD_Akoh7TqveaTkM-jBZG1084xwwNqYUs5RaI7GwfxiV7fxYwQngMrmgirVgS9lHk)**
Các bước hệ thống thực hiện validate:
	1. User cung cấp validate.
	2. Lấy mã `salt`  của user được lưu trong DB.
	3. Thực hiện mã hóa từ `password + salt` => `hash`
	4. So sánh `hash` tạo từ bước 3 và `hash` lưu trong DB. 

P/s:  Ngoài ra mọi người có thêm cơ chế nào khác để có thể lưu trữ pasword an toàn trong DB không? Nếu có hãy cmt cho mình biết với nha <3

### Tham khảo
- Free System Design - ByteByteGo - Trang 13
