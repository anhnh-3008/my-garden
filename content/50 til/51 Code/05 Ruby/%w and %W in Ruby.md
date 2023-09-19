---
title: "🌱 %w and %W in Ruby"
tags: [til, ruby]
date: 2023-01-10
---

## 🌿 What?

- 🌱 `%w` return an splited array from a input string by space.

```sh
irb> %w(I am from Vietnam)
#=> ["i", "am", "from", "Vietnam"]
```

- 🌱 `%W` is similar `%w` but allows receive interpolation value.

```sh
irb> country = "Vietnam" 
irb> %w(I am from #{country})
#=> ["i", "am", "from", "\#{country}"]

irb> %W(I am from #{country})
#=> ["i", "am", "from", "Vietnam"]
```

- 🌱 Similar with %q, %Q, %i, %I, ...

## 🌿 Refer 
- [https://til.hashrocket.com/posts/aqkz0yqdky-the-difference-between-w-and-w-in-ruby](https://til.hashrocket.com/posts/aqkz0yqdky-the-difference-between-w-and-w-in-ruby)