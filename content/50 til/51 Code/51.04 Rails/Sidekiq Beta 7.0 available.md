---
title: "🥋 Sidekiq Beta 7.0 available"
tags: [til, rails, sidekiq]
date: 2022-09-28
---

---

Hôm 2022-09-26 Author and Maintainer của Sidekiq **Mike Perham** đã cho ra mắt bản beta version 7.0 của **Sidekiq**. Đây được giới thiệu là một đợt big update với một vài tính năng siêu to và mới =)) một vài tính năng bị loại bỏ, một số API được cấu trúc lại và requirements được update.

## Version Support
---
- Required Redis 6.2+
- Required Ruby 2.7+
- Support for Rails 6.0+

## Upgrade
---
Nếu bạn muốn upgrade lên ver 7.0 để trải nghiệm và có cơ hội trở thành contributer cho **sidekiq** thì đừng ngần ngại mà hãy thêm dòng này vào Gemfile của mình nhé =))
```ruby
gem 'sidekiq', '< 8'
```

## What's new?
---

### Job Metrics
---
Version 7.0 sẽ add một tab metrics trên Web UI với high-resolution data cho thời gian excute job cũng như là khả năng đánh dấu thời điểm deploy. 
Mọi người có thể xem chi tiết tính năng này ở [Metrics](https://github.com/mperham/sidekiq/wiki/Metrics) 

### Embedding
---
Trước đây mọi người chỉ có thể khởi động **Sidekiq** bằng câu lệnh 
```sh
bundle exec sidekiq
```
Tính năng này theo tác giả có nói là một cách thử nghiệm để chạy **Sidekiq** thông qua việc gọi trực tiếp bằng những dòng code Ruby. Nó được gán nhãn thử nghiệm là vì có khả năng xung đột với plugins bên thứ 3 hay với chính hệ thống của bạn.
Mọi người có thể xem chi tiết tính năng này ở [Embedding](https://github.com/mperham/sidekiq/wiki/Embedding)

### Capsules
---
...

### redis-client
---
- **redis-client** là một Rubygem mới sử dụng giao thức RESP3 có trong Redis 6.0+.
- Sidekiq 6.5 đã giới thiệu về việc hỗ trợ cho gem **redis-client**  trong khi vẫn sử dụng gem **redis** là mặc định. Đến sidekiq 7.0 đã hoàn thiện việc chuyển đổi này và đã không còn sử dụng **redis** là mặc định nữa.
- **App của bạn vẫn có thể tiếp tục sử dụng redis**. 
- Hiện tại nếu bạn sử dụng **Sidekiq.redis** để truy cập vào kết nối Redis, API đó sẽ expose một connection dựa trên **redis-client**.

### redis-namespace
- 7.0 đã bỏ phần support cho **redis-namespace**. 

