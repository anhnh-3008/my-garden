---
title: "🌱 Delete git's branchs safely"
tags: [til, git]
date: 2022-12-21
---

## 🌿 What?

- 🌱 Sau một thời gian làm việc trên 1 repo git, chắc chắn chúng ta sẽ cần xóa đi những merged branchs hoặc những branchs không cần sử dụng tới nữa. Dưới đây là cách mình dùng để xóa đồng thời nhiều branchs có các partterns chung dưới local:

```sh
> git branch -D `git branch -a | grep merge`
```

- 🌱 Nhưng khi xóa các nhánh remote, cần bảo đảm an toàn, cẩn thận hơn nên mình sẽ bó cẩn thêm phần `confirmation`.

```sh
> git branch -a | grep remotes/anhnh-3008/deleted_branch | xargs -I % -p git push origin :%

> git push origin :remotes/sun/fixbug/game_room_controller ?... # y- Yes, n- No
```
