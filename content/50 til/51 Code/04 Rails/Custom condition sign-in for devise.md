---
title: "🌱 Custom condition sign-in for devise gem"
tags: [til, rails]
date: 2022-10-10
---

Mặc định khi đăng nhập, Devise sẽ tìm User dựa theo scope đã được thiết lập trong `config/initializers/devise.rb` 
Vd như đăng nhập theo email:

```rb
Devise.setup do |config|
  config.authentication_keys = [:v_code]
end
```

### 🌿  Vấn đề
- 🌱 Thế nhưng cuộc sống thường lắm gian truân và cuộc đời của mình cũng không ngoại lệ. 
- 🌱 Dự án của mình có đồng thời 2 cơ chế đăng nhập 1 là qua Devise, 2 là SSO thông qua bên thứ 3. Khi thực hiện SSO, hệ thống sẽ lưu user đó vào DB chung luôn và phân biệt bằng trường `provider`. Vấn đề là giờ phải xử lý sao cho khi đăng nhập với Devise, những thằng user do bên thứ 3 cung cấp không thể login vào được hệ thống.

### 🌿 find_for_database_authentication(warden_conditions)
- 🌱 Chúng ta có thể overwrite lại method `find_for_database_authentication` của Devise.
	- Method nhận vào scope chứa `authentication_keys`.
	- Output trả về một record tồn tại trong DB hoặc `nil`.

```rb
def find_for_database_authentication(warden_conditions)
  conditions = warden_conditions.dup
  # trim space and downcase
  email = conditions.delete(:email).strip.downcase
  find_by(email: email, provider: :traditional)
end
```


