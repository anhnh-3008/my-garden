---
title: "🌱 Some Tips for irb/rails console"
tags: [til, console]
date: 2022-10-31
---

### 🌿 Lấy giá trị output cuối cùng
- 🌱 `_` được gán giá trị là output mới nhất của irb/rails console.

```sh
> 1 + 1 
=> 2
> _
=> 2
```

### 🌿 Sandbox
- 🌱 Khi dùng option `--sandbox` các thay đổi đối với `atabase` sẽ được `rollback` khi thoát `rails console`.  

```sh
rails c --sandbox

> Account.first.destroy
=> true
> Account.find(1)
=> ActiveRecord::RecordNotFound: Could not find Account with id=1
> exit

rails c
> Account.find(1)
=> #<Account id: 1, ...>
```

### Tham khảo
- https://pragmaticstudio.com/tutorials/rails-console-shortcuts-tips-tricks