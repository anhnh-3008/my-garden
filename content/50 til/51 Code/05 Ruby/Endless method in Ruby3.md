---
title: "🌱 Endless method in Ruby3"
tags: [til, ruby]
date: 2023-01-31
---

## 🌿 What?
- 🌱 Từ vesion 3.0, Ruby cho phép định nghĩa những method đơn giản trên cùng một dòng giống endless condition.

```ruby
def isMan?(sex) = sex == 'man'

# isMan('man') => true
# isMan('female') => false

------------------------------------------------

# Method Setter không áp dụng được syntax này.
class A
  def attr=(val) = @attr = val
end
# => SyntaxError "setter method cannot be defined in an endless method definition"

------------------------------------------------

# Có thể  viết được nhiều dòng
def read(name) = File.read(name)
                     .split("\n")
                     .map(&:strip)
                     .reject(&:empty?)
                     .uniq
                     .sort
```

- 🌱 Ruby 3.0, endless method cần phải viết đầy đủ dấu ngoặc (, ), {, }. Vấn đề này đã được cải thiện ở version 3.1

```ruby
def log = puts "logging"
# 3.0: syntax error, unexpected string literal, expecting `do' or '{' or '('
# 3.1: successfully defined
```

## 🌿 Refer 
- Doc 3.0: https://rubyreferences.github.io/rubychanges/3.0.html#endless-method-definition
- Doc 3.1: https://rubyreferences.github.io/rubychanges/3.1.html#inside-endless-method-definitions-method-calls-without-parenthesis-are-allowed