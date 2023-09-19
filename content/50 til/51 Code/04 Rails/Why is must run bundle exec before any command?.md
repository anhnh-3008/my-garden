---
title: "🌱 why is must run bundle exec before any command?"
tags: [til, rails]
date: 2023-01-15
---

## 🌿 Issue

- 🌱 Trước làm dự án, lúc đầu mình chạy mỗi  `rspec` hay `rubocop` thì vẫn ô's kê mà sau lại phải thêm `bundle exec` ở đầu thì mới chạy được 🥵

## 🌿 Why?

- 🌱 Nếu chạy chay không dùng `bundle exec` hệ thống sẽ tìm trong PATH, nếu trong PATH có nhiều versions của 1 gem, nó có thể xảy ra việc sử dụng sai version.
- 🌱 `bundle exec`  để đảm bảo rằng version gem được sử dụng đúng với version gem chỉ định trong Gemfile chứ không phải là một version khác đã được cài trong hệ thống của chúng ta.

> Ví dụ như `rspec` trước đây mình chạy được là do máy của mình mới reset, chỉ có duy nhất 1 gem `rspec` được cài đặt cho dự án đang làm => chạy không bị lỗi. Vấn đề xảy ra khi mình cài thêm các versions `rspec` cho các projects khác => lệch version.

- 🌱 Theo mục đích trên, các câu lệnh không liên quan đến version gem, mình ko cần phải thêm `bundle exec` nữa. Ví dụ như `rails s` hoặc `rails db:create` ,...

## 🌿 Refer 
- [https://bundler.io/v2.4/man/bundle-exec.1.html](https://bundler.io/v2.4/man/bundle-exec.1.html)
