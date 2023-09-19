---
title: "🌱 Check prefix of string"
tags: [til, ruby]
date: 2022-10-13
cover: "00 Meta/01 Attachments/Open-Closed Principle.png"
---

### 🌿 What?
- 🌱 Trong Ruby, class `String` cung cấp method `start_with?` nhận vào những tiền tố mà bạn muốn xác định, trả về `true` nếu chuỗi kiểm tra bắt đầu bằng một trong những tiền tố đó.

```rb
string = "hello world"

string.start_with?("abc", "mentor") # => false
string.start_with?("zys", "hell")   # => true
```

- 🌱 Tham số:  
	- Phân biệt chữ Hoa và chữ thường
	- Nhận regex

```rb
string = "hello world"

string.start_with?("zys", "Hell") # => false
string.start_with?(/[\s\S]*/)     # => true
```

### 🌿 Refer
[https://til.hashrocket.com/posts/rettwv4dgl-check-if-string-starts-with-prefixes](https://til.hashrocket.com/posts/rettwv4dgl-check-if-string-starts-with-prefixes)