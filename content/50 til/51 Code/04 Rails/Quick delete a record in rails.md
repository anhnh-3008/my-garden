---
title: "🌱 Quick delete a recond in rails"
tags: [til, rails]
date: 2022-12-23
---

## 🌿 What?
- Trước đây khi muốn xóa một record, mình thường phải find trước xong mới xóa.

```rb
user = User.find(1)

user.destroy # xóa dependent và check callback
user.delete # xóa luôn, chả check chiếc gì hớt
```

- Nhưng từ Rails 6, nếu chúng ta chỉ muốn xóa record, có thể viết gọn hơn như sau:

```rb
User.destroy_by(id: 1) # xóa dependent và check callback
User.delete_by(id: 1) # xóa luôn, chả check chiếc gì hớt
```

- Cả hai không có khác nhau gì về hiệu suất. Đây chỉ là một phiên bản rút gọn cách viết thôi. 

## 🌿 Refer

- Mọi người có thể xem thêm code trong [Pull](https://github.com/rails/rails/pull/35316/files) này ạ.