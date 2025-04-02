---
title: 🌱 Browser Fingerprint - Canvas
tags:
  - til
  - antidetect
date: 2025-04-02
aliases:
  - browser fingerprint
draft: false
---

# 🌿 What?
Canvas là một HTML5 API, nó được sử dụng để vẽ (render) 2D để hiển thị lên Browser, ví dụ như một hình tròn, hình tam giác, render một đoạn chữ thành hình ảnh và nhiều thứ khác. Các hình 2D này hơi khác nhau ở các loại card màn hình (mắt thường khó có thể thể phân biệt) nên đây có thể sử dụng là một trong các thông số xác định sự khác nhau giữa các loại card màn hình.

# 🌿 How?
Antidetect sử dụng **kỹ thuật noise** làm nhiễu hình ảnh sau khi render, tạo sự khác biệt so với thông số thật của máy.

# 🚫 Nhược điểm
- Kỹ thuật noise sẽ có khả năng tạo ra tính duy nhất lớn.
- Hệ thống có big data sẽ nhận diện được điều đáng ngờ khi có người dùng đang có một fingerprint khác hoàn toàn so với hàng trăm triệu người dùng khác của hệ thống (Bạn không thể sử dùng một loại card màn hình, cài hệ điều hành và trình duyệt khác hoàn toàn so với hàng trăm triệu người dùng được, nếu trùng fingerprint có khi mới là bình thường).