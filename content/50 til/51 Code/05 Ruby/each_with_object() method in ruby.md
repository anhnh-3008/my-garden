---
title: "🌱 each_with_object in ruby"
tags: [til, ruby]
date: 2023-01-16
---

## 🌿 What?

- 🌱 `each_with_object` là method viết gọn cho TH chúng ta cần khởi tạo biến để lưu giá trị sau từng lần lặp. Tương tự như [[50 til/51 Code/05 Ruby/reduce() method in Ruby|reduce()]].

```rb
numbers = [1, 2, 3, 4, 5]

def specify_array(array)
  array.each_with_object([]) { |n, arr| arr << n if n > 3 }
end

specify_array(numbers)
=> [4, 5]
```

## 🌿 Compare with reduce()

- 🌱 Khác nhau về thứ tự tham số.

```rb
numbers = [1, 2, 3, 4, 5]

# initial object is first arg, second arg is array's element
sum_by_reduce = numbers.reduce(0) { |sum, num| sum + num }

# opposite to reduce() method
sum_by_each_with_object = numbers.each_with_object(0) { |num, sum| sum += num }
```

- 🌱 Thêm nữa là reduce sẽ trả về đối giá trị tích lũy còn each_with_object trả về object khởi tạo. Để ý syntax của 2 ví dụ trên, `each_with_object` phải sử dụng `+=` còn `reduce` thì không.
## 🌿 Refer 

- [https://ruby-doc.org/core-3.0.1/Enumerable.html#method-i-each_with_object](https://ruby-doc.org/core-3.0.1/Enumerable.html#method-i-each_with_object)