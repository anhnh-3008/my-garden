---
title: "🌱 visudo"
tags: [til, visudo]
date: 2022-11-08
---

- 🌱 Cấp quyền(cho user root, lệnh sudo, group admin) được cấu hình trong file `/etc/sudoers` .
	- Không bao giờ sử dụng trình soạn thảo văn bản thông thường(nano, vim, ...) để sửa `/etc/sudoers` , thay vào đó hãy dùng `visudo` .
	-  `visudo` validate cú pháp trước khi save file còn nano, vim, .... thì không, save mà sai syntax là oẳng luôn đó 🥵

- 🌱 Xem thêm: [https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file](https://www.digitalocean.com/community/tutorials/how-to-edit-the-sudoers-file)