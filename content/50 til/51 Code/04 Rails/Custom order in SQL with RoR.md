---
title: "🌱 Custom order in SQL with RoR"
tags: [til, rails]
date: 2022-11-14
---

- 🌱 `in_order_of` cho phép order theo thứ tự chỉ định trong SQL.

```rb
User.in_order_of(:id, [1, 5, 3])
# SELECT "users".* FROM "users"
#   ORDER BY FIELD("users"."id", 1, 5, 3)
#   WHERE "users"."id" IN (1, 5, 3)
```

- 🌱 [source code](https://github.com/rails/rails/blob/8015c2c2cf5c8718449677570f372ceb01318a32/activerecord/lib/active_record/relation/query_methods.rb#L447)

- 📑 FYI: Cách này trong SQL sẽ sort mà không sử dụng index. 

![[00 Meta/01 Attachments/Pasted image 20221114184148.png|800]]
