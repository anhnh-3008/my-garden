---
title: "🌱 reduce() method in Ruby"
tags: [til, ruby]
date: 2023-01-14
---

## 🌿 What?

- 🌱 `reduce` là method viết gọn cho TH chúng ta cần khởi tạo biến để lưu giá trị sau từng lần lặp.

```rb
numbers = [1, 2, 3, 4, 5]

def specify_array(arr)
  array = 0
  arr.each do |num|
    arr << num if num > 3
  end
  array
end

specify_array(numbers)
=> [4, 5]
```

- Sử dụng `reduce()`

```rb
numbers = [1, 2, 3, 4, 5]

def specify_array(array)
  array.reduce([]) { |arr, n| arr << n if n > 3 }
end

specify_array(numbers)
=> [4, 5]
```

## 🌿 Refer 
- https://apidock.com/ruby/Enumerable/reduce