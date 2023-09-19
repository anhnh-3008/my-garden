---
title: "🌱 Truncate by amount of word in Rails"
tags: [til, rails]
date: 2022-12-07
---

- 🌱 Rails cung cấp method truncate một chuỗi dựa theo số lượng từ. Ví dụ như chỉ muốn hiển thị 3 chữ đầu:

```rb
my_string = "một hai ba bốn năm!"
my_string.truncate_words(3)

#=> "một hai ba..."
```

- 🌱 Dấu 3 chấm tự động được thêm vào sau chuỗi đã được truncate. Chúng ta có thể custom bằng arg `omission` .

```rb
my_string.truncate_words(3, omission: " ... more")

#=> "một hai ba ... more"
```

- 🌱 Đương nhiên là cũng có truncate theo ký tự nữa, mọi người có thể đọc thêm ở [đây](https://apidock.com/rails/String/truncate).