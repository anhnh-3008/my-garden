---
title: "🌱 Amazon SSO - Single Sign-On Service"
tags: [aws]
date: 2023-04-13
alias: [aws sso]
---

## 🌿 What?
- Là dịch vụ cho phép đăng nhập một lần.
- Quan trọng, dịch vụ này còn cung cấp giải pháp quản lý quyền truy cập cho các accounts, roles, ...
- Có 3 kiểu xác định chính:
	- **Multi-Account Permission:**
		- Quán lý truy cập của nhiều accounts trong Organization của bạn.
		- Permission Sets - Là các bộ xác định quyền có thể sử dụng để assign cho các accounts.
	- **Application Assignment:**
		- Quản lý thông qua một bên thứ 3 kiểu Okta, Saleforce, ...
		- Bên thứ 3 sẽ cung cấp các thông tin như url, metadata, user info, ...
	- **Attribute-Base Access Control:**
		- Xác định quyền truy cập dựa vào attribute của account.
		- Vd quyền truy cập được xác định khác nhau với từng level account: junior, senior, expert,...

