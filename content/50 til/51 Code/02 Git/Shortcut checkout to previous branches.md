---
title: "🌱 Shortcut checkout previous branches"
tags: [git]
date: 2023-08-23
---

🌱 Với Git, chúng ta có thể checkout về các previous branches bằng cách sử dụng `@{-N} với N là số thứ tự nhánh muốn quay lại`  

- Ví dụ từ nhánh `master`, chúng ta checkout qua nhánh `branch-1`, sau đó đến `branch-2`
	- Checkout về `branch-1` : `git checkout -`
	- Hoặc checkout về `master` : `git checkout @{-2}`

🌱 Reference: [https://til.hashrocket.com/posts/xmki4qh2xg-git-checkout-to-previous-branches](https://til.hashrocket.com/posts/xmki4qh2xg-git-checkout-to-previous-branches)
