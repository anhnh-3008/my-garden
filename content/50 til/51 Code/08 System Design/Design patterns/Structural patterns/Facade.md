---
title: 🌱 Facade
tags:
  - til
  - design-patterns
date: 2023-11-15
aliases: 
draft: false
---
# 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20231115155148.png]]

> [!note] Định nghĩa
> **Facade** is a structural design pattern that provides a simplified interface to a library, a framework, or any other complex set of classes.

Facade là pattern sử dụng để cung cấp một interface đơn giản cho một hệ thống lớn hoặc một nhóm thao tác phức tạp, ví dụ như một lib, một framework hay sự kết hợp của nhiều classes trong hệ thống.

Đặc điểm:
- Đơn giản hoá khi sử dụng.
- Giấu đi các chi tiết triển khai, phức tạp của hệ thống. Chỉ hiển thị những gì người dùng cần sử dụng thôi.
- Tính linh hoạt và bảo trì: có thể thay đổi cách triển khai bên trong mà không ảnh hưởng đến phần code gọi Facade.

![[00 Meta/01 Attachments/Pasted image 20231115155428.png]]

Ví dụ trong thực tế, sàn thương mại điện tử cũng là một Facade pattern.
Khi đặt một món hàng, chúng ta chỉ cần nhấn vào nút mua, chọn số lượng và điền địa chỉ là xong(áp mã giảm giá nữa 😗). Nhưng để đơn hàng đến được với người mua, sàn thương mại điện tử sẽ thực hiện một chuỗi những tác vụ như xác nhận với người bán còn hàng không, kiểm 
hàng, đóng gói hàng, đến lấy hàng, thuế, ...

# 🛠️ Implement with Ruby
Pattern sử dụng khi mình muốn kết hợp nhiều tác vụ vào một chỗ. Ví dụ như hệ thống cho xe oto, khi khởi động xe sẽ kết hợp cả bật điều hoà và nhạc.

```ruby
# Subsystem 1
class Engine
  def start
    puts "Engine started"
  end
end

# Subsystem 2
class AirConditioner
  def turn_on
    puts "Air conditioner turned on"
  end
end

# Subsystem 3
class MusicPlayer
  def play_music
    puts "Music playing"
  end
end

# Facade
class CarFacade
  def initialize
    @engine = Engine.new
    @ac = AirConditioner.new
    @music_player = MusicPlayer.new
  end

  def start_car
    @engine.start
    @ac.turn_on
    @music_player.play_music
    puts "Car is ready to go"
  end
end

# Client code
car_facade = CarFacade.new
car_facade.start_car
```
# 🌿 Refer
- https://refactoring.guru/design-patterns/facade
