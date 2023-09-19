---
title: "🌱 Credential file in Rails"
tags: [til, rails]
date: 2022-12-02
---

> [!question] Question
> 
> Khi khởi tạo một project, Rails sẽ tự động tạo ra file **credentials.yml.enc** trong folder **config**. Khi click vào xem nội dung thì chỉ có mỗi một dòng hash dài ngoằng ngoẵng. Thế nó sinh ra để làm gì nhỉ 🤔

- 🌱 Từ sau Rails 5.2, khi init project sẽ tự động tạo file `config/credentials.yml.enc` chứa hash được mã hóa bởi [aes-128-gcm](https://www.cryptosys.net/pki/manpki/pki_aesgcmauthencryption.html)  để lưu những thông tin "nhạy cảm" của dự án. 

- 🌱 Rails sẽ dùng `config/master.key` hoặc `ENV["RAILS_MASTER_KEY"]` để mã hóa nội dung. Vì đã được mã hóa nên file `config/credentials.yml.enc` vẫn có thể public, miễn là chúng ta không làm lộ `master key` là được.

- 🌱 Mặc định file tạo ra sẽ chỉ lưu `secret_key_base` của Rails app. Tuy nhiên chúng ta có thể edit thêm thông tin bằng command:

```sh
$ rails credentials:edit
```

> [!info] Info
> 
> 📝 Câu lệnh trên sẽ tạo file **config/credentials.yml.enc** và   **config/master.key** nếu chưa tồn tại hoặc chưa được định nghĩa.
> 
> Tìm hiểu thêm: **rails credentials:help**  

- 🌱 Đọc thông tin mã hóa bằng câu lệnh:

```sh
> Rails.application.credentials
```

![[00 Meta/01 Attachments/Pasted image 20221202152110.png|800]]

> [!danger] Danger
> 
> Tuyệt đối không được làm mất hay public master key! 

- 🌱 Source: https://guides.rubyonrails.org/security.html#custom-credentials
