---
title: "🌱 Custom direct URL by Routes in Rails"
tags: [til, rails]
date: 2022-11-03
---

### 🌿 What?
- 🌱 Rails cung cấp `direct` giúp chúng ta xác định một `route` `redirect` đến một URL bất kỳ. 

```rb
# config/routes.rb
Rails.application.routes.draw do
	direct :get_to_my_blog do
		"https://nhanh.netlify.app"
	end
end
```

- 🌱 Trong Rails ta sẽ có route `get_to_my_blog_url` gọn gàng đẹp đẽ. 
- 🌱 Ngoài ra có thể thêm điều kiện để  get URL.

```rb
# config/routes.rb
Rails.application.routes.draw do
	direct :get_to_the_goog, search: nil do |options| 
		"https://google.com/search?q=#{options[:search]}"
	end
end

get_to_the_goog_url(search: "stackoverflow")
```

- 🌱 `Direct` sẽ không hiển thị routes khi chúng ta gõ `rails routes`. Chúng ta sẽ vẫn có `_path` helper nhưng ko nên sử dụng vì nó cắt mất cái tên miền đấy 😂. 
- 🌱 Ngoài ra `direct` không dùng được trong `namespace` hoặc `scope`. Nếu đặt nhầm thì rails sẽ `raise exception`.

### 🌿 Refer
- https://guides.rubyonrails.org/v5.2/routing.html#direct-routes