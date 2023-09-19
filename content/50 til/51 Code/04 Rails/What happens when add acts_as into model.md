---
title: 🌱 What happens when add acts_as into model
tags:
  - til
  - rails
date: 2023-01-16
draft: true
---

> [!question] Q?
> 
> Khi dùng gem paranoia để xóa mềm, chúng ta phải thêm acts_as_paranoid vào model. Vậy acts_as_paranoid tác động gì đến model của chúng ta?  

## 🌿 What?

- 🌱 Trong Rails, `acts_as_xyz` sẽ bổ sung thêm những methods(thường sẽ là method class) cho model chứa nó thông qua các modules và mixins, ví dụ như sắp xếp thứ tự của list, filter theo điều kiện nào đó, ...
- 🌱 Các acts_as gems sẽ cần chỉ định trước các cột trong bảng, ví dụ như gem `paranoia` mặc định là cột `deleted_at`.

