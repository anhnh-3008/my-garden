---
title: "🌱 Find by Regex in VsCode"
tags: [til, utils]
date: 2022-11-30
---


## 🌿 Vấn đề

🌱 Tôi có một file cần xóa nhiều dòng thừa có cấu trúc giống nhau (dòng trống, dòng comment ,...) trong VsCode.

## 🌿 Giải pháp

- 🌱 Trong thanh tìm kiếm của VsCode, có option tìm kiếm theo regex. Nếu muốn xóa dòng trống,  `Ctrl + H` -> thêm regex `^$\n` -> `Ctrl + Alt + Enter ` là xong.

![[00 Meta/01 Attachments/Pasted image 20221130152936.png]]

- 🌱 Option rất tiện khi chúng ta muốn tìm những giá trị có format giống nhau(số điện thoại, email, etc ...) 