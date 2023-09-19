---
title: "🌱 _in_ and _out_ of Pry"
tags: [til, rails]
date: 2022-11-17
---

### 🌿 What?
- 🌱 Trong Pry, các giá trị `input`, `output` sẽ tự động được lưu trong 2 array có thể truy cập được đó là `_in_` và `_out_`. Số lượng phần tử cache của 2 cu này được định nghĩa ở `Pry.config.memory_size`(mặc định là 100 phần tử). Nếu hết dung lượng, những giá trị mới sẽ được ghi đè.

```sh
pry(main)> 1
=> 1
pry(main)> 2
=> 2
pry(main)> 3
=> 3
pry(main)> _in_
=> #<Pry::Ring:0x0000562f98b2ce88 @buffer=[nil, "1\n", "2\n", "3\n", "_in_\n"], @count=5, @max_size=100, @mutex=#<Thread::Mutex:0x0000562f98b2ce60>>
pry(main)> _out_
=> #<Pry::Ring:0x000055d4e3002b80 @buffer=[nil, 1, 2, 3, #<Pry::Ring:0x000055d4e3002b80 ...>], @count=5, @max_size=100, @mutex=#<Thread::Mutex:0x000055d4e3002b58>>
pry(main)> _out_.to_a[1] + _out_.to_a[2]
=> 3
```

### 🌿 Refer
- 🌱 Mọi người có thể đọc thêm ở  [document](https://github.com/pry/pry/wiki/Special-Locals#the-input-and-output-cache)
