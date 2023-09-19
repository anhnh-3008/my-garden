---
title: 🌱 Why must run apt update before install any lib for Linux
tags:
  - til
  - os
date: 2022-11-18
---

[Câu trả lời](https://askubuntu.com/questions/337198/is-sudo-apt-get-update-mandatory-before-every-package-installation)

- 🌱 Lệnh `apt update` sẽ cập nhật danh sách mới nhất các packages có trong kho Ubuntu.

> [!info] Info
> 
> Danh sách repo được lưu trong file **/etc/apt/sources.list**

- 🌱 Lệnh `apt install` sẽ đọc trong danh sách packages được cập nhật ở lệnh `apt update` gần nhất.

- 🌱 Nếu chắc chắn package chuẩn bị install đã nằm trong danh sách cập nhật, việc chạy `apt update` có vẻ là hơi thừa 😶 Cơ mà thay vì ngồi xác định như thế thì mình chọn chạy `apt update` cho đỡ mệt mọi 😆

