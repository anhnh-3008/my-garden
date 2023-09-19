---
title: "🌱 Floating-point error"
tags: [til, ruby]
date: 2022-12-13
---

## 🌿 What?

-   Trong các ngôn ngữ lập trình, khi tính toán với float hoặc double thì sẽ gặp sai số. VD:

```rb
1.9 + 1.2
=> 3.0999999999999996
```

- Với những ngành như tài chính, tiền bạc mà tính lệch một số sau dấu phẩy thôi là tới công chiện liền 🥵

## 🌿 Solution

- Trong DB chúng ta hay dùng `decimal` với 2 thông số `precision(số lượng chữ số tính cả sau dấu ,)` và `scale(số lượng chữ số sau dấu ,)` để tính toán.
- Còn khi chúng ta thao tác ở bên ngoài, ví dụ như trong code hoặc console thì có thể sử dụng BigDecimal.

```rb
BigDecimal("1.2") + BigDecimal("1.9")
=> 0.31e1

_.to_f
=> 3.1
```


## 🌿 Refer 

-   [https://spin.atomicobject.com/2014/08/14/currency-rounding-errors/](https://spin.atomicobject.com/2014/08/14/currency-rounding-errors/)
-   [https://ttuan.xyz/til/computer/floating_point_math/](https://ttuan.xyz/til/computer/floating_point_math/)
-   https://www.youtube.com/watch?v=PZRI1IfStY0&ab_channel=Computerphile