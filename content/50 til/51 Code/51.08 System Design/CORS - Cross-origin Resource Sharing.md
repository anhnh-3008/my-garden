---
title: "📑 CORS - Cross-origin Resource Sharing"
tags: [til, sys design, web policy]
date: 2022-10-01
---

## What?
---
`CORS`  là một cơ chế cho phép chia sẻ nhiều tài nguyên(images, files, fonts, javascript,...) giữa nhiều trang web khác nhau.

## Why?
---
CORS ra đời do sự xuất hiện của [[50 til/51 Code/51.08 System Design/Same-origin policy]].

## How?
---
`CORS` sử dụng các HTTP Header để thông báo với trình duyệt nhận request là 'Em là con ông A nhà bà B ở cuối làng, anh cho em vào lấy ít đồ cho bố em nhé ' =))
`Access-Control-Allow-Origin`  ở header mà trường này ko có giá trị hoặc giá trị ko hợp lệ thì sẽ bị báo lỗi.
