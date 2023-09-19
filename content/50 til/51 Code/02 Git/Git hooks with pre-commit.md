---
title: "🌱 Git hooks with pre-commit"
tags: [til, git]
date: 2022-11-21
---

- 🌱 Để tránh tình trạng gặp phải **stupid mistakes** như push code lên mà có cả `byebug`, `binding.pry`, `debugger`, ... Git cho phép chúng ta sử dụng `hooks` để kiểm tra tự động những vấn đề ntn 🥳

- 🌱 Tất cả các hooks của 1 repo được lưu trong folder `.git/hooks`

![](00%20Meta/01%20Attachments/Pasted%20image%2020221121182121.png)

- 🌱 Tạo file `.git/hooks/pre-commit`. Có thể viết bằng bất kỳ `script language(như Ruby, Python, JS, ...)` nào chúng ta muốn.

```sh
#!/bin/sh

FILES_PATTERN='\.?$'

FORBIDDEN='binding.pry\|byebug\|console.log'

git diff --cached --name-only | \
    grep -E $FILES_PATTERN | \
    xargs grep --color --with-filename -n $FORBIDDEN && \
    echo 'COMMIT REJECTED' && \
    exit 1

exit 0
```

- 🌱 Bạn có thể custom những từ khóa không muốn push lên repo thông qua biến `FORBIDDEN`.

![](00%20Meta/01%20Attachments/Pasted%20image%2020221121182849.png)