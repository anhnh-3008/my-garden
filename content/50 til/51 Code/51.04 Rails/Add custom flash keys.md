---
title: "🥦 Add custom flash keys"
tags: [til, rails, flash]
date: 2022-10-07
---

---

`ActionController::Base` mặc định cung cấp key `:notice` cho `#redirect_to`   
```ruby
  class flash_demo
    if true
      redirect_to root_path, notice: "Notice"
    else
      flash[:error] = "Error"
      redirect_to root_path
    end
  end
```

Nhưng nếu bạn muốn thêm `:error` như `:notice` thì có thể thử cách này nhé!
```ruby
  class flash_demo
    add_flash_types :error
    
    if true
      redirect_to root_path, notice: "Notice"
    else
      redirect_to root_path, error: "Error"
    end
  end
```

Refer: [add_flash_keys](https://til.hashrocket.com/posts/ouyfd1cpfu-add-custom-flash-keys)