---
title: 🌱 New syntax of ActiveRecord::QueryMethods Select
tags:
  - til
  - rails
date: 2023-05-30
aliases: []
---

🌿 Before:
```rb
User.joins(:posts)
    .select("user.id as user_id, users.name as user_name,
             posts.id as post_id, posts.title as post_title")
```

🌿 After:
```rb
User.joins(:posts)
    .select(
      users: {id: :user_id, name: :user_name},
      posts: {id: :post_id, title: :post_title}
    )
```

🌿 SQL Query:
```
SELECT "users"."id" AS user_id, "users"."name" AS user_name, "posts"."id" AS post_id, "posts"."title" AS post_title
FROM "users"
INNER JOIN "posts" ON "post"."user_id" = "users"."id"
LIMIT $1  [["LIMIT", 11]]
```

🌱 Refer: [https://blog.saeloun.com/2022/09/07/activerecord-select-adds-support-for-hash-values-in-rails-7/](https://blog.saeloun.com/2022/09/07/activerecord-select-adds-support-for-hash-values-in-rails-7/)