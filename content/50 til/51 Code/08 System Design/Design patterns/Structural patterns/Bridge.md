---
title: 🌱 Bridge
tags:
  - til
  - design-patterns
date: 2023-11-16
aliases: 
draft: false
---
# 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20231116103112.png]]

> [!note] Định nghĩa
> **Bridge** is a structural design pattern that lets you split a large class or a set of closely related classes into two separate hierarchies—abstraction and implementation—which can be developed independently of each other.

Bridge là pattern sử dụng để tách biệt **abstraction** và **implementation**. Để 2 phần có thể phát triển độc lập mà không ảnh hưởng gì đến nhau, từ đó giúp hệ thống linh hoạt và dễ mở rộng hơn.

# 💡Abstraction and Implementation
Theo ý hiểu của mình:
- Abstraction được sử dụng để xây dựng những thứ người dùng có thể thấy được. Xét trong một application, có thể hiểu abstraction như GUI.
- Implementation thì được xây dựng để cung cấp những phương thức hoạt động cho các đối trượng Abstraction đã defined. Xét trong một application, có thể hiểu implementation như API.

# 🚧 Problem
Giả sử chúng ta cần build một hệ thống có khả năng vẽ nhiều hình(chữ nhật, tròn, ...) + tô màu.
![[00 Meta/01 Attachments/Pasted image 20231116111821.png]]

Nếu gộp tất cả dô class Shape thì số lượng subclasses sẽ nhiều lên khi chúng ta thêm hình mới hoặc màu mới. Ví dụ như trên mà thêm hình tam giác là phải tạo thêm 2 classes: BlueTriangle và ReadTriangle, chưa kể còn thêm màu Green nữa thì ê hề 😅
# 🛠️ Implement with Ruby
![[00 Meta/01 Attachments/Pasted image 20231116111542.png]]

Giải pháp cho trường hợp trên là chúng ta sẽ tách riêng biệt phần tạo hình(**abstraction**) và phần tô màu ra riêng(**implementation**). Như thế này thì khi thêm màu mới hoặc hình mới thì chỉ cần thêm duy nhất một class tương ứng thôi.

```ruby
# Implementation interface
class Color
  def apply_color
    raise NotImplementedError, "#{self.class} has not implemented method '#{__method__}'"
  end
end

# Concrete Implementations
class RedColor < Color
  def apply_color
    "Red"
  end
end

class GreenColor < Color
  def apply_color
    "Green"
  end
end

# Abstraction
class Shape
  attr_reader :color

  def initialize(color)
    @color = color
  end

  def draw
    raise NotImplementedError, "#{self.class} has not implemented method '#{__method__}'"
  end
end

# Refined Abstractions
class Circle < Shape
  def draw
    "Drawing a circle with color: #{color.apply_color}"
  end
end

class Square < Shape
  def draw
    "Drawing a square with color: #{color.apply_color}"
  end
end

# Usage
red_circle = Circle.new(RedColor.new)
green_square = Square.new(GreenColor.new)

puts red_circle.draw
# => "Drawing a circle with color: Red"
puts green_square.draw
# => "Drawing a square with color: Green"
```

# 🌿 Refer 
https://refactoring.guru/design-patterns/bridge