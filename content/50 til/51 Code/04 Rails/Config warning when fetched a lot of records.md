---
title: "🌱 Config warning when fetched a lot of records"
tags: [til, rails]
date: 2022-10-20
---

 - 🌱 Từ Rails 5 chúng ta đã có thể thêm config `warn_on_records_fetched_greater_than`:  hiển thị cảnh báo trong `rails server` hoặc `rails console` khi có số lượng câu queries lớn hơn số lượng chúng ta đã chỉ định.

```rb
# config/environments/development.rb

# Show warn if fetch greater than 50 records
config.active_record.warn_on_records_fetched_greater_than = 50
```

![[00 Meta/01 Attachments/01.02 TIL/Server/Config warning when fetched a lot of records/Pasted image 20221020091559.png]]