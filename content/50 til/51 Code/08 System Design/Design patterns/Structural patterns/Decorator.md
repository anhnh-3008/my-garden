---
title: 🌱 Decorator
tags:
  - til
  - design-patterns
date: 2023-11-13
aliases: 
draft: false
---
# 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20231115152309.png]]

> [!note] Định nghĩa
> **Decorator** is a structural design pattern that lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.


Decorator là một pattern cho phép mở rộng chức năng mới của một object mà không làm ảnh hưởng đến cấu trúc đã có sẵn.

![[00 Meta/01 Attachments/Pasted image 20231115152451.png]]

Ví dụ như khi bạn thấy trời bắt đầu hơi lạnh, bạn có thể mặc thêm một chiếc áo len. Khi lạnh hơn nữa, bạn có thể khoác thêm một cái áo khoác. Và khi trời mưa bạn có thể trùm thêm một cái áo mưa. Khi không sử dụng nữa, bạn có thể dễ dàng bỏ nó đi.
# 🚧 Problem
Ví dụ bạn có đối tượng là coffee, lúc đầu bạn chỉ có một loại coffee nguyên chất nên chỉ có giá mặc định là 1$. Nhưng do nhu cầu của khách hàng, quán của bạn có thêm cả coffee thêm sữa, coffee thêm đường.

# 🛠️ Implement with Ruby
```ruby
class Coffee
  def cost
    5
  end

  def description
    'Simple coffee'
  end
end

# Decorator base class
class CoffeeDecorator < Coffee
  def initialize(coffee)
    @coffee = coffee
  end

  def cost
    @coffee.cost
  end

  def description
    @coffee.description
  end
end

# Concrete decorator class - Milk
class MilkDecorator < CoffeeDecorator
  def cost
    @coffee.cost + 2
  end

  def description
    @coffee.description + ', with milk'
  end
end

# Concrete decorator class - Sugar
class SugarDecorator < CoffeeDecorator
  def cost
    @coffee.cost + 1
  end

  def description
    @coffee.description + ', with sugar'
  end
end

# Sử dụng
simple_coffee = Coffee.new
# => simple_coffee.description = 'Simple coffee'

milk_coffee = MilkDecorator.new(simple_coffee)
# => simple_coffee.description = 'Simple coffee, with milk'

sugar_milk_coffee = SugarDecorator.new(milk_coffee)
# => simple_coffee.description = 'Simple coffee, with milk, with sugar'
```

# 🌿 Reference
- https://refactoring.guru/design-patterns/decorator