---
title: "🌱 Operator += and << with string"
tags: [til,ruby]
date: 2022-11-15
---

- 🌱 Trong Ruby, hãy nối chuỗi bằng `<<` thay vì `+=`!
	- `+=` sẽ tạo ra một object mới sau khi nối chuỗi.

```rb
name = "Hoang"

name.object_id
=> 71860

name += " Anh"

name.object_id
=> 71880
```

- 🌱 `<<` sẽ nối chuỗi trực tiếp trên object cũ, không tạo ra object mới. Cải thiện performance khi thao tác với những chuỗi lớn.

```rb
name = "Hoang"

name.object_id
=> 71900

name << " Anh"

name.object_id
=> 71900
```

