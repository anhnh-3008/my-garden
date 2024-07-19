---
title: 🌱 Chap 2 - Tạo class có một trách nhiệm duy nhất
tags:
  - system_design
date: 2024-07-18
aliases: 
draft: false
---
# 🌿 Là gì?
- Một class chỉ có một trách nhiệm duy nhất và thực hiện một nhiệm vụ duy nhất.

# ❓Tại sao cần áp dụng?
- Dễ thay đổi và tránh bị ảnh hưởng bởi những thay đổi trong tương lai.
- Tái sử dụng được.

# 🏗️ Áp dụng
Hãy cùng làm rõ ưu điểm và cách thức triển khai một class single responsibility thông qua ứng dụng thiết kế **một chiếc xe đạp**:

> [!question] Vấn đề
> Thiết kế đối tượng mô phỏng chiếc xe đạp có khả năng custom size của bánh răng và xích xe đạp.
> 
> Giả sử bạn có thể thay đổi kích thước của bánh răng và xích xe đạp để phù hợp với nhu cầu sử dụng như đi lên dốc thì dùng bánh răng to và xe dây xích bé để đạp tốn ít sức hơn, ngược lại khi đi đường bằng thì dùng bánh răng nhỏ và dây xích to để bánh sau đi được nhiều vòng hơn trong 1 chu kỳ đạp.

![[00 Meta/01 Attachments/Pasted image 20240718171553.png]]


### Tạo một lớp Gear cơ bản
- Với yêu cầu, chúng ta sẽ tạo một class Gear có thuộc tính là chainring(dây xích) và cog(bánh răng) và một phương thức trả về tỷ lệ giữa hai thuộc tính trên.
```ruby
class Gear
	attr_reader :chainring, :cog
	def initialize(chainring, cog)
	    @chainring = chainring
		@cog = cog
	end

	def ratio  
		chainring / cog.to_f
	end
end

puts Gear.new(52, 11).ratio # -> 4.72727272727273
puts Gear.new(30, 27).ratio # -> 1.11111111111111
```

Sau đó, khách hàng muốn thêm tính năng tính kích thước của của bánh xe(kích thước bao gồm cả bánh răng + vành + lốp xe). Đơn giản thôi:

```ruby
class Gear
	attr_reader :chainring, :cog, :rim, :tire
	def initialize(chainring, cog)
	    @chainring = chainring
		@cog = cog
		@rim = rim
		@tire = tire
	end

	def ratio  
		chainring / cog.to_f
	end

	def gear_inches  
		# tire goes around rim twice for diameter
		ratio * (rim + (tire * 2))
	end
end

puts Gear.new(52, 11, 26, 1.5).gear_inches # -> 137.090909090909
puts Gear.new(52, 11).ratio # -> Raise Exception
```

### 🚨 Vấn đề
- Với việc sửa đổi phương thức khởi tạo của Gear, phương thức `ratio` chúng ta tạo trước đó sẽ gặp lỗi và chúng ta sẽ phải sửa lại toàn bộ những chỗ có sử dụng `ratio`.
- Nhưng vì class Gear quá nhỏ và chúng ta có thể xử lý được các ảnh hưởng nên hiện tại cơ bản đã tạo xong class Gear.

> [!question] Câu hỏi?
> Liệu đây có phải là cách tổ chức code tốt? 

> [!answer] Trả lời
> Đây chưa phải là cách tổ chức code hợp lý vì: có sự phụ thuộc trong class Gear. Nếu trong tương lai Gear tiếp tục có những thay đổi, khối lượng xử lý ảnh hưởng cũng sẽ tăng lên.

> [!tip] Tại sao Single Responsibility lại quan trọng?
> - Các ứng dụng dễ thay đổi sẽ được tạo nên bởi các classes dễ tái sử dụng. Các classes dễ tái sử dụng là các classes có hành vi xác định rõ ràng và ít sự ràng buộc.
> - Một lớp có nhiều trách nhiệm sẽ khó tái sử dụng. Dẫn đến các tình huống tồi tệ hơn như copy phần code cần sử dụng qua một nơi khác(vi phạm DRY) hay đôi khi phải sửa class vì một lý do gián tiếp. Chung quy lại là chi phí khi cần mở rộng hoặc sửa đổi.

### ❓Làm sao để xác định một lớp chỉ có một trách nhiệm duy nhất?
- Mô tả các hành vi của class, nếu xuất hiện từ 'và' hay từ 'hoặc' thì class đang có nhiều hơn 1 trách nhiệm.
- Theo tác giả, các nhà thiết kế hướng đối tượng sử dụng từ `cohesion(tính kết dính)` để mô tả khái niệm này. Trong [[50 til/51 Code/01 Style/SOLID|SOLID]], nguyên tắc đầu tiên là Single Responsibility Principle - SRP. SRP không yêu cầu 1 class chỉ được định nghĩa 1 hành vi duy nhất, thay vào đó, có thể có nhiều hành vi và các hành vi phải phục vụ một mục đích cốt lõi của class.
- Ví dụ như class Gear, chỉ định nghĩa các hành vi liên quan đến bộ phận trong hộp gear như dây xích và bánh răng. Hành vi tính lốp xe, vành không liên quan, không nên định nghĩa trong Gear.

### 🚧 Viết code dễ dàng thay đổi
Có thể trong giai đoạn phát triển hiện tại, chúng ta không biết tương lai sẽ có những tính năng gì mới nhưng phải luôn có mindset là sẽ có thêm code, mình cần phải chuẩn bị cho điều đó. 
Các phương pháp để thực hiện điều này:
#### Phụ thuộc vào hành vi, không phải dữ liệu.
- Nên nhớ, các đối tượng giao tiếp với nhau thông qua hành vi(phương thức). Sau này cần thay đổi chỉ cần thay đổi ở trong phương thức là xong. Tránh dùng dữ liệu, sau muốn đổi giá trị lại phải sửa ở nhiều nơi.

#### Ẩn biến instance
- Cái này giống vụ setup getter/setter bên java, trong ruby có thể implement nhanh 2 methods trên với `attr_accessor`. Cái này cũng giống ý trên, mục tiêu vẫn là wrap dữ liệu vào trong methods, khi gọi đến dữ liệu sẽ chỉ gọi thông qua getter, giả sử muốn thay đổi giá trị thì chỉ cần sửa trong getter thôi.

#### Ẩn cấu trúc dữ liệu
- Các dữ liệu có cấu trúc phức tạp, nên định nghĩa một phương thức xử lý cấu trúc đó. Khi những chỗ khác cần sử dụng dữ liệu sẽ gọi qua phương thức xử lý cấu trúc. Ý này nó cũng giống ý ẩn biến thôi 😄.
- Ví dụ bạn có dữ liệu là một mảng 2 chiều chưa giá trị của rim và tire:
```ruby
class ObscuringReferences attr_reader :data  
	def initialize(data)
		@data = data
	end

	def diameters  
		# 0 is rim, 1 is tire data.collect {|cell|
		cell[0] + (cell[1] * 2)}
	end
end

# rim and tire sizes (now in millimeters!) in a 2d array 2
@data = [[622, 20], [622, 23], [559, 30], [559, 40]]
```
- Giả sử giờ ta có thêm một hàm cũng cần sử dụng @data, hàm đó vẫn sẽ sử dụng 0 là rim và 1 là tire như diameters. Vấn đề xảy ra khi cần sửa đổi, mảng sẽ lưu thêm giá trị thứ 3, thứ tự của rim và tire cũng bị thay đổi => chúng ta sẽ phải thay đổi ở tất cả các nơi có sử dụng @data. Thay vào đó:
```ruby
class ObscuringReferences attr_reader :data  
	def initialize(data)
		@wheels = wheelify(data)
	end

	def diameters
		wheels.collect {|wheel|
			wheel.rim + (wheel.tire * 2)}
	end

	Wheel = Struct.new(:rim, :tire)
	
	def wheelify(data)
		data.collect {|cell| Wheel.new(cell[0], cell[1])}
	end
end
```
 - Chúng ta sẽ có riêng hàm wheelify chịu trách nhiệm xử lý cấu trúc của @data, nếu cần sửa đổi gì @data thì chỉ sửa ở đây thôi.

> [!tip] Tip
> ⭐⭐⭐ Phụ thuộc vào hành vi, không phụ thuộc vào dữ liệu

#### Single Responsibility
Luôn có mindset ***chỉ một trách nhiệm duy nhất*** với classes và với cả các methods. Có thể cải tiến tiếp đoạn code trên như sau:
```ruby
class ObscuringReferences attr_reader :data  
	def initialize(data)
		@wheels = wheelify(data)
	end

	def diameters
		wheels.collect {|wheel| diameter(wheel)}
	end

	def diameter(wheel)
		wheel.rim + (wheel.tire * 2)
	end

	Wheel = Struct.new(:rim, :tire)
	
	def wheelify(data)
		data.collect {|cell| Wheel.new(cell[0], cell[1])}
	end
end
```

##### 🌟 Lợi ích đạt được
- Các phương thức rõ ràng.
- Không cần sử dụng comment.
- Khuyến khích contributors tái sử dụng.
- Dễ sử dụng với các classes khác.

> [!tip] Tip
> Nếu bạn cần dùng chú thích cho một phương thức nào đó, hãy tách nhỏ phương thức đó ra.


### 🏁 Áp dụng các điều trên áp dụng cải tiến class Gear ban đầu
```ruby
class Gear
	attr_reader :chainring, :cog, :rim, :tire
	def initialize(chainring, cog, wheel = nil)
	    @chainring = chainring
		@cog = cog
		@wheel = wheel
	end

	def ratio  
		chainring / cog.to_f
	end

	def gear_inches  
		# tire goes around rim twice for diameter
		ratio * wheel.diameter
	end
end

class Wheel  
	attr_reader :rim, :tire

	def initialize(rim, tire)
		@rim = rim  
		@tire = tire
	end

	def diameter  
		rim + (tire * 2)
	end

	def circumference
		diameter * Math::PI
	end
end

@wheel = Wheel.new(26, 1.5)
puts @wheel.circumference # -> 91.106186954104
puts Gear.new(52, 11, @wheel).gear_inches # -> 137.090909090909
puts Gear.new(52, 11).ratio # -> 4.72727272727273
```

# 🌿 Refer 
Chap 2 - Practical Object-Oriented Design in Ruby