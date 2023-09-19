---
title: "🌱  Save serialized object to the database"
tags: [til,rails]
date: 2022-12-30
---

## 🌿 What?
- Như mọi người đã biết, chỉ trong Postgresql chúng ta mới có thể lưu Array vào db còn MySQL thì chịu chết. Trong Rails nếu muốn làm việc trên, tôi thường viết custom attribute trong model để xử lý dữ liệu.

```rb
# models/user.rb

class User
  def codes
    codes.split(',') #phone_numbers in db = "123,345,567" 
  end 
end
```

## 🌿 Serialization of ActiveRecord
-   Rails cung cấp một  Instance Public methods là serialize để giúp chúng ta thực hiện việc lưu serialized object(như Array, Hash, YAML, JSON) và tự động convert về đúng kiểu dữ liệu khi truy xuất.
-   Params của method:
	-   **attr_name:** Tên attribute cần lưu serialized object
	-   **class_name_or_coder:** Optional, chỉ định kiểu dữ liệu
		-   Mặc định là YAML, ngoài ra có thể chọn Array, Hash, và JSON
		- **_custom coder:_** _Có thể tự define kiểu dữ liệu (xem them ở_ _[doc](https://api.rubyonrails.org/classes/ActiveRecord/AttributeMethods/Serialization/ClassMethods.html#method-i-serialize)__)_
-
```rb
# models/user.rb

class User
  serialize:codes
end

3.1.2 :001 > Comment.create! user_id: 1, content: [1,2,3]
#<Comment:0x00007fdf8dd6dac0                                   
 id: 1,                                                        
 content: [1, 2, 3],
 ...
```

## 🌿 Refer
-   [Serialize Document](https://api.rubyonrails.org/classes/ActiveRecord/AttributeMethods/Serialization/ClassMethods.html#method-i-serialize)