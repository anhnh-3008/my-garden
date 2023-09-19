---
title: "🌱 Combine arrays in Ruby"
tags: [til, ruby]
date: 2023-01-12
---

## 🌿 What?

- 🌱 Trong quá trình làm dự án, mình cần build dữ liệu cho `f.select` từ 2 mảng lấy được từ server, ruby cung cấp method `.zip` để kết hợp mảng.

```rb
ids = [1,2,3,4]
address = ['a', 'b', 'c', 'd']

ids.zip(address)
=> [[1,'a'],[2,'b'],[3,'c'], [4,'d']]
```

- 🌱 Trường hợp cần kết hợp đầy đủ tất cả các cases từ các phần tử của mảng, sử dụng `Enumerator.product`.
- Ví dụ như web bán quần áo, cta có mảng Size và mảng Brand, vì mới bán nên các Brand vẫn còn đủ các size.

```rb
sizes = ['small', 'medium', 'large']
brands = ['adidas', 'nike', 'puma', 'lv']

Enumerator.product(sizes, brands)
=> [
  ['small', 'adidas'],
  ['small', 'nike'],
  ['small', 'puma'],
...
  ['large', 'puma'],
  ['large', 'lv']
]
```