---
title: "🌱 frozen_string_literal in rails"
tags: [til, rails]
date: 2022-11-22
---

### 🌿 What?
- 🌱 Rubocop có rule check khai báo `frozen_string_literal: true` cho từng file, nhưng nó để làm gì?

- 🌱 `frozen_string_literal` là một **magic comments** có từ Ruby 2.3, nó giúp tối ưu bộ nhớ cũng như cải thiện performance bằng việc **cung cấp vùng nhớ dựa theo nội dung của string**(nội dung giống nhau sẽ chung 1 vùng nhớ), tương tự như `:symbol`. Ngoài ra, sử dụng comment trên cũng sẽ ngăn chặn việc thay đổi string.

```rb
# test.rb
# frozen_string_literal: true 
p 'name'.object_id
p 'name'.object_id

str  =  'hello'
str  <<  ' world'

p str
```

```sh
> ruby test.rb
60
60
Traceback (most recent call last):
test.rb:6:in `<main>': can't modify frozen String: "hello" (FrozenError)
```

- 🌱 Nếu trong file `frozen`, chúng ta vẫn muốn một string động, có thể khai báo:

```rb
str = String.new('hello')
str << ' world'
```

### 🌿 Refer
- 🌱 [Tham khảo](https://www.mikeperham.com/2018/02/28/ruby-optimization-with-one-magic-comment/)
