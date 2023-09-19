---
title: "🌱 Pattern matching in Ruby"
tags: [til, ruby]
date: 2023-01-30
---

## 🌿 What?

- 🌱 Pattern matching là feature được thử nghiệm từ Ruby2.7 và được áp dụng chính thức từ version 3.0, cho phép dễ dàng match giá trị với pattern.

```ruby
if "123" in /\A\d+\z/
  p "It's a string of only digits"
end

# => It's a string of only digits
```

### Các pattern được hỗ trợ:
1. 🌱 Array pattern: `[<subpattern>, <subpattern>, <subpattern>, ...]`.

- Kiểm tra mảng chỉ chứa pattern 2 integers liền kề không:

```ruby
case [1, 2, 3]
in [Integer, Integer]
  "matched"
else
  "not matched"
end
#=> "not matched"
```

- Hoặc chỉ cần phần tử đầu tiên là integer:

```ruby
case [1, 2, 3]
in [Integer, *]
  "matched"
else
  "not matched"
end
#=> "matched"
```

2. 🌱 Find pattern: `[*variable, <subpattern>, <subpattern>, <subpattern>, ..., *variable]`. **(Find pattern is experimental)**

- Kiểm tra mảng có chứa 2 chuỗi liền kề không:

```ruby
case ["a", 1, "b", "c", 2]
in [*, String, String, *]
  "matched"
else
  "not matched"
end
#=> matched
```

3. 🌱 Hash pattern: `{key: <subpattern>, key: <subpattern>, ...}`.

```ruby
case {a: 1, b: 2, c: 3}
in {a: Integer}
  "matched"
else
  "not matched"
end
#=> "matched"
```

4. 🌱 One-line pattern matching with `=>`.

- Gán giá trị cho một biến nếu phần tử match với pattern:

```ruby
case [1, 2]
in Integer => a, Integer
  "matched: #{a}"
else
  "not matched"
end
#=> "matched: 1"

case {a: 1, b: 2, c: 3}
in a: Integer => m
  "matched: #{m}"
else
  "not matched"
end
#=> "matched: 1"
```

## 🌿 Refer 
- Document: https://docs.ruby-lang.org/en/3.0/syntax/pattern_matching_rdoc.html