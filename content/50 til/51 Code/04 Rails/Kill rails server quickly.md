---
title: "🌱 Kill rails server quickly"
tags: [til, rails]
date: 2022-11-29
---

### 🌿 Vấn đề
- 🌱 Khi làm việc với rails, chắc hẳn đã có lần chạy server bạn đã gặp lỗi này.

![[00 Meta/01 Attachments/Pasted image 20221129232330.png]]

- 🌱 Sau khi chạy `rails s`, file `tmp/pids/server.pid` được tự động sinh ra, lưu Process ID(PID) của server đang chạy. Nguyên nhân xảy ra lỗi trên có thể là do chẳng may crash server(mất điên, máy lag) hay bất kì tình huống nào khác mà rails chưa kịp kill server cho chúng ta.

### 🌿 Giải pháp

- 🌱 Để giải quyết, tôi hay xóa xừ cái file `server.pid`.

```sh
rm -rf tmp/pids/server.pid
```

- 🌱 Sau đó thêm alias trong `.bashrc` để đỡ phải gõ nhiều 😄

```sh
# /.bashrc

alias kars="rm -rf tmp/pids/server.pid"
```