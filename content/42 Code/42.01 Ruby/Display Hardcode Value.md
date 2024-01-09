---
title: 🌱 Display Hardcode Value
tags:
  - ruby
  - rails
date: 2022-10-31
aliases: 
draft: false
---
![[00 Meta/01 Attachments/Pasted image 20230919152349.png]]

Trong quá trình phát triển các dự án Ruby on Rails, mình thấy [gem config](https://github.com/rubyconfig/config) rất hay được sử dụng để lưu các giá trị hardcode.

Vấn đề mình gặp đó là mỗi lần muốn xem giá trị từ một key ví dụ như `Settings.status.unprocessable_entity` là mình phải mở cái file `settings.yml` lên dò dò trong đấy rất mất thời gian. Nên mình có viết một extension trên VsCode, khi mình hover vào đoạn text có cú pháp của gem config, VsCode sẽ hiển thị 1 popup chứa giá trị hardcode trong file setting.

![](https://raw.githubusercontent.com/anhnh-3008/display-hardcode-value/anhnh-3008-add-issue-bug-template/media/demo-display-hardcode-value.gif)

Nếu thấy có ích, bạn có thể download trên VsCode với ID là `anhnh-3008.display-hardcode-value` nha.

Version require của VsCode là `>= 1.72.0`