---
title: "🌱 Get last occurrence of value in an array"
tags: [til, ruby]
date: 2022-11-25
---

- 🌱 Trong Ruby, hàm `rindex` nhận vào một giá trị và trả về index cho lần cuối cùng giá trị đó xuất hiện trong array.

```rb
arr= ['b', 'a', 'a', 'a']
arr.rindex('a')
#=> 3

arr.rindex('b')
#=> 0
```

