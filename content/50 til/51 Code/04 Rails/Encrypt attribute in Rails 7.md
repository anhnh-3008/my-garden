---
title: "🌱 Encrypt attribute in Rails 7"
tags: [til, rails]
date: 2022-12-02
---

> [!question] Question
> 
> Rails 7 vừa ra mắt **Active Record Encryption**, cho phép **encrypt data** ở trên tầng **Application**. Nhưng nó đem lại tác dụng gì khi chúng ta đã **encrypt data** ở tầng **Database** rồi nhỉ 🤔. 

## 🌿 Why?
- 🌱 Khi có hacker chiếm được quyền hệ thống, snapshot database hoặc application logs sẽ chỉ hiển thị dữ liệu đã được mã hóa.

- 🌱 Ngăn ngừa lập trình viên sơ xuất để lộ dữ liệu nhạy cảm thông qua application logs.

- 🌱 Ngăn truy xuất dữ liệu trong Rails console nếu không có bộ keys để giải mã.

## 🌿 How?
### Setup
- Tạo keys:

```sh
$ rails db:encryption:init
```

- Thêm keys vào [[50 til/51 Code/04 Rails/Credentials file in Rails| credentials file]].

### Declare attribute
- Định nghĩ trong modal trường encrypts.

```rb
class User < ApplicationRecord
  encrypts :email
end
```

- Khi tạo user, giá trị của email đã được mã hóa.  

![[00 Meta/01 Attachments/Pasted image 20221202182529.png|800]]

> [!info] Info
> 
> Không thể find_by theo thuộc tính được mã hóa. 
> 
> Nếu vẫn muốn truy vấn theo thuộc tính, hãy thêm option 
**deterministic: true**

```rb
class User < ApplicationRecord
  encrypts :email, deterministic: true
end
```

### 🌿 Refer
- 🌱 https://guides.rubyonrails.org/active_record_encryption.html