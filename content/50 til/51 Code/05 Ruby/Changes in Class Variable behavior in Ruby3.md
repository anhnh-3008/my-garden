---
title: "🌱 Changes in Class Variable behavior in Ruby3"
tags: [til, ruby]
date: 2023-01-31
---

## 🌿 What?
- 🌱 Ở Ruby 2.7, class variable được sử dụng chung giữa class cha và các class con. Do có thể overwrite ở bất cứ đâu nên sẽ khó để tracking hoặc debug.

- 🌱 Đến Ruby 3.0, class variable chỉ có thể overwrite ở các Class con kế thừa hoặc ở chính Class đó.

```ruby
class Dog
  @@color = ['yellow']

  # bad practice
  def self.overwrite_legs!
    @@legs = 4
  end
  
  def self.overwrite_legs!
    @@color
  end
end

class Husky < Dog
  @@legs = 2

  def self.show_legs
    @@legs
  end

  # good practice
  def self.add_color
    @@color.push 'green'
  end
end

#=> Dog.overwrite_legs!
#=> 4
#=> Husky.show_legs
#=> in `show_legs': class variable @@legs of Husky is overtaken by Dog (RuntimeError)

--------------------------

#=> Husky.add_color
#=> ["yellow", "green"]
#=> Dog.show_color
#=> ["yellow", "green"]
```


## 🌿 Refer 
- Document: https://rubyreferences.github.io/rubychanges/3.0.html#changes-in-class-variable-behavior