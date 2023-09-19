---
title: "🌱 Show entire length of output in Rspec"
tags: [til, rspec]
date: 2022-12-23
---

## 🌿 Issues
- Khi chạy test case compare 2 objects, trong trường hợp không match + object dài, output lỗi sẽ hiển thị rút gọn như dưới đây(mặc định sẽ hiển thị 200 kí tự cho từng object).

![[00 Meta/01 Attachments/Pasted image 20221223163807.png]]

## 🌿 Solution 
- Set `RSpec::Support::ObjectFormatter.default_instance.max_formatted_output_length = nil`  để show đầy đủ thông tin của 2 objects.
- Hoặc
```rb
RSpec.configure do |rspec|
  rspec.expect_with :rspec do |config|
    config.max_formatted_output_length = nil
  end
end
```

![[00 Meta/01 Attachments/Pasted image 20221223163953.png]]

## 🌿 Refer

- [Code Rspec xử lý độ dài output](https://github.com/rspec/rspec-expectations/blob/ae06ba1535fca7c0ce4014d7d05fae823e6be9d4/lib/rspec/expectations/configuration.rb#L70)
