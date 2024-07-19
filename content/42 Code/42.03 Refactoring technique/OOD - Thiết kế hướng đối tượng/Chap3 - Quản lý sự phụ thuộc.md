---
title: 🌱 Chap 3 - Quản lý sự phụ thuộc
tags:
  - system_design
date: 2024-07-19
aliases: 
draft: false
---
# 🌿 Là gì?
- Trong lập trình hướng đối tượng, các Objects giao tiếp với nhau thông qua hành vi, phương thức. Ở [[42 Code/42.03 Refactoring technique/OOD - Thiết kế hướng đối tượng/Chap 2 - Tạo class có một trách nhiệm duy nhất|Chap 2 - Tạo class có một trách nhiệm duy nhất]], chúng ta đã biết sự cần thiết của việc định nghĩa single responsibility class là như thế nào. Và vì mỗi class chỉ làm một nhiệm vụ nên bắt buộc chúng cần phải giao tiếp với nhau để xử lý các nhiệm vụ phức tạp hơn.
- Để giao tiếp với nhau, object cần biết các objects khác có nhiệm vụ gì? Và chính việc này tạo ra sự phụ thuộc. Hãy quay trở lại với ví dụ tạo class Gear và Wheel.

```ruby
class Gear
  attr_reader :chainring, :cog, :rim, :tire

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog = cog
    @rim = rim
    @tire = tire
  end

  def gear_inches
    ratio * Wheel.new(rim, tire).diameter
  end

  def ratio
    chainring / cog.to_f
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
end
```

## Nhận biết sự phụ thuộc
- Theo thiết kế trên, Gear sẽ phụ thuộc Wheel ở những điểm sau:
	- Gear biết sự tồn tại của Wheel
	- Gear biết object của Wheel sẽ phản hồi cho hành vi diameter.
	- Gear biết Wheel khởi tạo với 2 tham số là rim và tire.
	- Gear biết thứ tự của tham số truyền vào Wheel là rim trước, tire sau.
![[00 Meta/01 Attachments/Pasted image 20240719162007.png]]

>[!danger] Tác hại
> Ràng buộc sẽ dần biến những liên kết trở nên chặt chẽ, các lớp sẽ như một khối thống nhất. Gây khó khăn cho việc tái sử dụng, sửa đổi cũng như mở rộng. 

> [!note] Note
> Không thể tránh sự phụ thuộc giữa các objects, nhiệm vụ của chúng ta là giảm thiểu điều đó. Tránh tạo ra Sự Ràng Buộc, đó là khi sửa class A mà bắt buộc phải sửa cả class B hay tệ hơn là C, D, ... 😅

> [!tip] Tip
> Hãy giữ cho các class của chúng ta biết ít nhất có thể, đừng biến chúng trở thành những kẻ nhiều chuyện 🙅‍♂️🙅‍♂️🙅‍♂️
# 🛡️ Các phương pháp để tránh phụ thuộc

## 💉 ⭐⭐⭐ Inject Dependencies
> [!note] Định nghĩa
> Nhận thể hiện(instance) của các lớp khác thông qua tham số. Tránh khởi tạo instance của các lớp khác trong định nghĩa lớp.

Quay trở lại với đoạn code `Gear` và `Wheel` bên trên, chúng ta có thể thấy khi thay đổi `Wheel` thì phương thức `gear_inches` cũng sẽ phải thay đổi. Nhưng vấn đề lớn hơn đó là phương thức `gear_inches` có sự ràng buộc đó là chỉ tính được kích thước của `Wheel`. Hãy tưởng tượng sau này chũng ta cần tính toán kích thước của các gear khác như disks chẳng hạn(cũng có `diameter` như `Wheel`), phương thức `gear_inches` sẽ không đáp ứng được.

`Gear` không cần biết `Wheel`, không cần biết `Wheel` khởi tạo với 2 tham số là `rim` đứng đầu và `tire` đứng sau. `Gear` chỉ cần biết nhận vào các đối tượng sẽ phản hồi phương thức `diameter`.

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring, cog, wheel)
    @chainring = chainring
    @cog = cog
    @wheel = wheel
  end

  def gear_inches
    ratio * wheel.diameter
  end

  def ratio
    chainring / cog.to_f
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
end
```

Vậy là chỉ qua việc sử dụng kỹ thuật **Inject Dependencies**, `Gear` từ có 4 phụ thuộc với `Wheel` hiện tại đã không còn phụ thuộc vào liên quan giữa hai lớp. `Gear` bây giờ chỉ cần biết là sẽ nhận những đối tượng có phản hồi phương thức `diameter`. Còn đối tượng đấy là gì thì: 'không phải chuyện của tôi 🤷‍♂️🤷‍♂️🤷‍♂️'

> [!note] Ghi chú
> Kỹ thuật Inject Dependencies loại bỏ phụ thuộc một class cần biết tên hay cách thức khởi tạo của một class khác.


## ⭐⭐⭐ Isolate Dependencies(cô lập các phụ thuộc)
Trong trường hợp vì một lý do nào đó mà chúng ta không thể sử dụng phương pháp **Inject Dependencies** (có thể là có quá nhiều chỗ cần sửa đổi, ảnh hưởng rộng). Chúng ta có thể cân nhắc phương pháp cô lập sự phụ thuộc.

> [!note] Định nghĩa
> Cô lập sự phụ thuộc ở một phương thức riêng và chỉ sử dụng phụ thuộc thông qua phương thức đó.
### 1. Cô lập phụ thuộc khởi tạo
Trong Ruby có thể triển khai theo 2 cách:
```ruby
class Gear
  attr_reader :chainring, :cog, :rim, :tire, :wheel

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog = cog
    @wheel = Wheel.new(rim, tire)
  end

  def gear_inches
    ratio * wheel.diameter
  end
  ...

```

> [!warning] Lưu ý
> Cách trên sẽ khởi tạo đồng thời object của Wheel mỗi lần object Gear được khởi tạo.

Cách 2 cải tiến hơn cách 1, sử dụng lazy-load
```ruby
class Gear
  attr_reader :chainring, :cog, :rim, :tire

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog = cog
  end

  def gear_inches
    ratio * wheel.diameter
  end

  def wheel
    @wheel ||= Wheel.new(rim, tire)
  end
  ...

```
Cách này, object `Wheel` sẽ chỉ được khởi tạo khi được gọi trong phương thức `gear_inches`.

### 2. Cô lập phụ thuộc hành vi
Đơn giản thôi, các hành vi của Class khác thì mình cho vào một phương thức riêng.
```ruby
class Gear
  attr_reader :chainring, :cog, :rim, :tire

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog = cog
  end

  def gear_inches
    ratio * diameter
  end

  def wheel
    @wheel ||= Wheel.new(rim, tire)
  end

  def diameter
    wheel.diameter
  end
  ...

```
Tất nhiên là không sớm thì muộn, chúng ta cũng sẽ viết phương thức diameter như trên để DRY code. Nhưng ngoài việc để code đỡ bị lặp, phương thức còn mang lại giá trị tuyệt vời hơn. Giả sử như nếu sau này Wheel có sửa đổi diameter thì tất cả các ảnh hưởng sẽ được hạn chế ở trong chính phương thức này. Okela đấy chứ 😎

### 3. Loại bỏ phụ thuộc thứ tự tham số
```ruby
class Gear
  attr_reader :chainring, :cog, :wheel
  def initialize(chainring, cog, wheel)
    @chainring = chainring
    @cog       = cog
    @wheel     = wheel
  end
  ...
end

Gear.new(
  52,
  11,
  Wheel.new(26, 1.5)).gear_inches
```
Như ví dụ trên, các đối số là bắt buộc và chúng cần phải được tuân theo đúng thứ tự. Trong quá trình phát triển, nếu cần thay đổi thứ tự tham số trong phương thức khởi tạo, chúng ta sẽ phải sửa ở tất cả những nơi khởi tạo đối tượng trong dự án.
Không may, điều này thường xuyên xảy ra, nhất là ở giai đoạn đầu của quá trình phát triển.

> [!danger] Bad Case
Tệ hơn, chúng ta còn tránh việc thay đổi thứ tự các tham số chỉ để không phải sửa lại những nơi khởi tạo đối tượng, mặc dù điều đó là cần thiết.

💡 Giải pháp: thay việc truyền tham số thông qua các keys.
```ruby
class Gear
  attr_reader :chainring, :cog, :wheel
  def initialize(chainring:, cog:, wheel:)
    @chainring = chainring
    @cog       = cog
    @wheel     = wheel
  end
  ...
end

Gear.new(
  chainring: 52,
  cog: 11,
  wheel: Wheel.new(26, 1.5)).gear_inches
```

🚧 Trường hợp tham số của chúng ta nhiều và có thể sẽ thay đổi trong tương lai, hãy sử dụng hash.
```ruby
class Gear
  attr_reader :chainring, :cog, :wheel
  def initialize(args)
    @chainring = args[:chainring]
    @cog       = args[:cog]
    @wheel     = args[:wheel]
  end
  ...
end

Gear.new(
  :chainring => 52,
  :cog       => 11,
  :wheel     => Wheel.new(26, 1.5)).gear_inches
```

### 4. Xử lý giá trị mặc định
Khi nhận hash làm tham số khởi tạo, chúng ta có thể chỉ định các giá trị mặc định theo cách sau:
```ruby
def initialize(args)
  @chainring = args.fetch(:chainring, 40)
  @cog       = args.fetch(:cog, 18)
  @wheel     = args[:wheel]
end
```

Không nên sử dụng cú pháp:
```ruby
@bool = args[:boolean_thing] || true
```
'||' sẽ kiểm tra nếu giá trị là nil hoặc false thì sẽ gán giá trị mặc định. Nếu trong trường hợp chúng ta muốn truyền giá trị là false thì cách này không sử dụng được.

🌱 Trong trường hợp bạn có nhiều keys và phải set nhiều giá trị mặc định, hãy sử dụng cách này để dễ quản lý default value và phương thức khởi tạo trông bớt rối:
```ruby
def initialize(args)
  args = defaults.merge(args)
  @chainring = args[:chainring]
  @cog       = args[:cog]
  @wheel     = args[:wheel]
  # ...
end

def defaults
  { :chainring => 40, :cog => 18 }
end
```

### 5. Cô lập phụ thuộc khởi tạo đối tượng của bên thứ 3
Chúng ta sẽ bàn tiếp đến trường hợp giả sử class `Gear` thuộc về một bên thứ 3 và chúng ta không thể sửa đổi trực tiếp trên class `Gear` như các trường hợp bên trên được. Nhiệm vụ của chúng ta sẽ là cô lập sự khởi tạo của `Gear` để tránh ảnh hưởng khi `Gear` thay đổi.
```ruby
module GearWrapper
  def self.gear(args)
    SomeFramework::Gear.new(args[:chainring], args[:cog], args[:wheel])
  end
end

# Sử dụng GearWrapper để tạo thể hiện Gear
gear = GearWrapper.gear(
  chainring: 52,
  cog:       11,
  wheel:     Wheel.new(26, 1.5)
)
```

> [!note] Ghi chú
> Trong OOD, thuật ngữ Factory được sử dụng để gọi các module như GearWrapper. Chỉ những đối tượng có nhiệm vụ khởi tạo một đối tượng khác.

>[!tip] Lưu ý
>- GearWrapper là module vì chúng ta không cần tạo các thể hiện từ GearWrapper. Chúng ta chỉ cần GearWrapper xử lý hành vi tạo object Gear.

> [!tip] Tip
> Những gì thuộc về 'bên thứ 3' nên được xử lý bọc lại ở một nơi duy nhất.
# 🌿 Refer 
Chap 3 - Managing Dependencies
