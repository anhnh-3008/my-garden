---
title: "🌱 How to safely remove a column in Rails? "
tags: [til, rails]
aliases: [rails, migrate, best practice]
date: 2022-10-13
---

### 🌿 What?
- 🌱 Rails cung cấp method `ignored_columns` để xóa tạm thời một cột trong DB, sau khi sửa logic xong xuôi chúng ta mới thực hiện migrate, tránh việc migrate đi migrate lại, deploy nhiều lần(nếu cột đã có trên môi trường STG/PROD).

### 🌿 How?
- 🌱 Step 1️⃣: Set ignore cột cần xóa trong model.

```rb
class User < ActiveRecord::Base
  self.ignored_columns = [:username]
end
```

- 🌱 Step 2️⃣: Kiểm tra xem cột `username` đã được xóa tạm thời chưa.

```rb
User.first.username

=> raises exception NoMethodError
```

- 🌱 Step 3️⃣: Thay đổi logic code liên quan đến trường `username`.

- 🌱 Step 4️⃣: Deploy lên các môi trường, test/fix những "lỗi lầm" nếu có.

- 🌱 Step 5️⃣: Thêm migrate xóa cột `username` .

### 🌿 Refer
🌵 [https://newsletter.shortruby.com/p/how-to-safely-remove-a-column-in](https://newsletter.shortruby.com/p/how-to-safely-remove-a-column-in)