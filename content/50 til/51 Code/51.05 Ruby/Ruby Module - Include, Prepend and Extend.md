---
title: "🥦 Ruby Module: Include, Prepend and Extend"
tags: [til, ruby]
date: 2022-10-25
---

## 🌿 Ancestors chain
- Khi khởi tạo một Class, mỗi Class sẽ có một `ancestors chain` - là danh sách các classes và modules mà nó được kế thừa hoặc imported.
Trong Ruby có 3 cách để import Module cho 1 Class.

### 🌱 Include
- Method trong module sẽ trở thành `instance method` của Class.
- Thứ tự trong `ancestors chain`: `Class` > `Module/Class imported` > `Superclass`.  

```rb
module A
	def say
		p 'hello'
	end	
end

class B
	include A
end
```

``` sh
> B.new.say
=> "hello"
>
> B.ancestors
=> [B, A, ..., Object, ..., BasicObject]
```

### 🌱 Prepend
- Giống `include`, khác thứ tự được thêm vào trong `list ancestors`.
- Thứ tự trong `ancestors chain`: `Module/Class imported` > `Class` > `Superclass`.

```rb
module A
	def say
		p 'hello'
	end	
end

class B
	prepend A
end
```

``` sh
> B.new.say
=> "hello"
>
> B.ancestors
=> [A, B, ..., Object, ..., BasicObject]
```

### 🌱 Extend
- Method trong module trở thành `class method` của Class.
- Import methods của module vào `ancestors chain` của `singleton class` của class extend.

```rb
module C
	def say
		p 'hello'
	end	
end

class D
	extend C
end
```

``` sh
> D.new.say
=> undefined method 'say' ...
>
> D.say
=> "hello"
>
> D.ancestors
=> [D, ..., Object, ..., BasicObject]
>
> D.singleton_class.ancestors
=> [#<Class:D>, C, ...] 
```


### Tham khảo
- https://medium.com/@leo_hetsch/ruby-modules-include-vs-prepend-vs-extend-f09837a5b073