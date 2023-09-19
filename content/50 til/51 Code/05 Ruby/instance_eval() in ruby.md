---
title: "🌱 instance_eval() in ruby"
tags: [til, ruby]
date: 2023-01-13
---

## 🌿 What?

- 🌱 Trong Ruby, class Object có public method là `instance_eval()`, method này cấp quyền truy cập tới các biến instance của object, nhận vào string chứa code Ruby hoặc block và excute theo context của object.

```rb
class Klass
  def initialize
    @secret = 99
  end
end

irb(main):001:0> k = Klass.new
irb(main):002:0> k.instance_eval { @secret }
=> 99
```

```rb
# add method
string = "String"
string.instance_eval do
  def new_method
    self.reverse
  end
end

irb(main):033:0> string.new_method
=> "gnirtS"
```

- 🌱 Tương tự với module và class sẽ có `module_eval()` và `class_eval()`

## 🌿 Refer 
- [https://apidock.com/ruby/Object/instance_eval](https://apidock.com/ruby/Object/instance_eval)
