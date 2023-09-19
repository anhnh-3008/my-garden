---
title: "🌱 Delegate in Rails"
tags: [til, rails]
date: 2022-12-19
---

## 🌿 Issues

- Khi code RoR, mình thường xuyên sử dụng delegate trong các dự án. Nhưng nay tự nhiên có anh hỏi mình mấy câu như delegate là cái gì? tại sao phải dùng? nên dùng thế nào cho hợp lý? thì mình lại có sự ngập ngừng nhẹ 😅. Tiện đây mình lược lại một lần sau đi khè cho trôi chảy 😆 Let's gooo!!  

## 🌿 What?

- Theo APIdock:
> Provides a [delegate](https://apidock.com/rails/Module/delegate) class method to easily expose contained objects’ public methods as your own.

- `Delegate` hỗ trợ một object truy xuất dễ dàng các public methods của một object khác như chính các methods của nó.


## 🌿 Why?

> The Law of Demeter Principle – LoD, còn gọi khác là nguyên tắc Demeter hay nguyên tắc “càng biết ít càng tốt” hay nguyên tắc “Một dấu chấm”. Nó **là một nguyên tắc thiết kế để phát triển phần mềm, đặc biệt là các chương trình hướng đối tượng**

- Delegate giúp code của cta tuân thủ theo nguyên tắc trên.

## 🌿 How?

- Có 3 options:
1. `:to` - chỉ định object cần truy xuất public methods(có thể nhận nhiều giá trị).

```rb
class A < ActiveRecord::Base
	has_many :Bs
end

class B < ActiveRecord::Base
	belongs_to :A

	delegate :name, :description, to: :A
end

pry(main)> B.first.name
=> "A"
pry(main)> B.first.description
=> "Description of A"
```

2. `:prefix` - chỉ định tiền tố.

```rb
class A < ActiveRecord::Base
	has_many :Bs
end

class B < ActiveRecord::Base
	belongs_to :A

	delegate :name, :description, to: :A, prefix: 'A'
end

pry(main)> B.first.A_name
=> "A"
pry(main)> B.first.A_description
=> "Description of A"
```

3. `:allow_nil` - nếu flag=true, không raise [DelegationError](https://apidock.com/rails/Module/DelegationError)

```rb
class A < ActiveRecord::Base
	has_many :Bs
end

class B < ActiveRecord::Base
	belongs_to :A

	delegate :name, :description, to: :A, prefix: 'A', allow_nil: true
end

# allow_nil: false - default
pry(main)> B.first.A_name
=> Module::DelegationError: B#A_name ...

# allow_nil: true
pry(main)> B.first.A_name
=> "A"
```

## 🌿 Refer 
- https://apidock.com/rails/Module/delegate