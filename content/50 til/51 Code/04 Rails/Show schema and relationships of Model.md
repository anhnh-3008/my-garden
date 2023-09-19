---
title: "🌱 Show schema and relationships of Model"
tags: [til, rails]
date: 2022-12-09
---

## 🌿 What?
- 🌱 Gem pry-rails cung cấp method `show-models` hiển thị schema và relationships của tất cả Model trong DB.

```rb
> pry(main)> show-models
> WhitelistedJwt
	  id: integer
	  jti: string
	  aud: string
	  exp: datetime
	  refresh_token: string
	  account_id: integer
	  device_id: integer
	  created_at: datetime
	  updated_at: datetime
	  refresh_token_exp: datetime
	  active_flag: boolean
	  belongs_to :account
	  belongs_to :device
> Schedule
	  id: integer
	  jti: string
	  aud: string
	  exp: datetime
	  refresh_token: string
...
```

- 🌱 Nếu DB nhiều model, chúng ta có thể chỉ định riêng model cần xem.

```rb
pry(main)> show-model Project
```

- 🌱 Dùng `--grep` để tìm theo partial. Trả về Model chưa partial truyền vào.

```rb
pry(main)> show-models --grep aud
```

## 🌿 Refer 
Mình quên mất tiêu 😅