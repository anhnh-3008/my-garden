---
title: "🌱 Split array by condition in Ruby"
tags: [til, ruby]
date: 2022-12-05
---

### 🌿 What?
- 🌱 Từ 2.5.1, Ruby cung cấp method `partition`, chia 1 mảng thành 2 mảng con dựa theo điều kiện truyền vào.

```rb
(1..6).partition { |v| v.even? }
#=> [[2, 4, 6], [1, 3, 5]]

['', '1', '12', '123', '1234'].partition { |v| v.length > 2 }
#=> [['123', '1234'], ['', '1', '12']]
```

### 🌿 Refer
- 🌱 Link doc: [Enumerable#partition](https://ruby-doc.org/core-2.5.1/Enumerable.html#:~:text=partition%20%7B%20%7Cobj%7C%20block%20%7D%20%E2%86%92%20%5B%20true_array%2C%20false_array%20%5D)
