---
title: "🌱 Validate numeric in rails"
tags: [til, rails]
date: 2022-12-21
---
## 🌿 Issues
- Option `only_integer` được dùng để validate chỉ nhận giá trị integer. Nhưng mình muốn nhận được cả giá trị float và integer cơ 😅

## 🌿 Solutuion
- Theo [doc](https://edgeguides.rubyonrails.org/active_record_validations.html#numericality), option `only_integer` validate format theo regex `/\A[+-]?\d+\z`.
- Nếu muốn pass các giá trị float, có thể thay thế format regex `/\A-?(?:\d+(?:\.\d*)?|\.\d+)\z/`

```ruby
validates :number, format: { with: /\A-?(?:\d+(?:\.\d*)?|\.\d+)\z/ }
```

- Hoặc Rails 7 đã thêm option `only_numeric` để giải quyết vấn đề trên.

```ruby
validates :number, numericality: { only_numeric: true }
```

## 🌿 Refer 
- [Pull add opion to numericality validator](https://github.com/rails/rails/pull/43914/files)