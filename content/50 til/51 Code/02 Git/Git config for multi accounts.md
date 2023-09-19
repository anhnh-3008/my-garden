---
title: "⚙️ Git config for multi accounts"
tags: [til, git]
date: 2022-09-29
---

## 🌿 Vấn đề
 - Bài viết này ra đời khi mình bị các anh ngồi cạnh 'cười chê' do dùng nhiều accounts git trên cùng một máy nhưng lại switch bằng cơm =))) Sau khi khóc xong thì mình có tìm hiểu cách config để thuận tiện hơn cho việc sử dụng.

## 🌿 Giải pháp
- 🌱 Ý tưởng là mình sẽ chia ra làm 2 thư mục **work** và **personal**  để sử dụng cho các repo tương ứng.
- 🌱 Ở file **.gitconfig** global set user mặc định và điều hướng config riêng cho từng folder.
``` git
# .gitconfig

[user]
  name = anhnh-1028
  email = nguyen.hoang.anh-c@sun-asterisk.com

[includeIf "gitdir:~/personal/"]
  path = ~/personal/.gitconfig-personal

[includeIf "gitdir:~/work/"]
  path = ~/work/.gitconfig-work
```
- 🌱 Set user cho từng folder
```git
# ~/work/.gitconfig

[user]
  name = anhnh-1028
  email = nguyen.hoang.anh-c@sun-asterisk.com

# ~/personal/.gitconfig
[user]
  name = anhnh-3008
  email = mail-personal@gmail.com
```
- 🌱 Xong phần config thông tin, giờ đến phần ssh. Skip bước gen ssh-key + add key lên git, giờ mình set [[50 til/51 Code/06 Servers/Config SSH]] thôi.

```git
# ~/.ssh/config

Host git-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/ssh-key-work

Host git-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/ssh-key-personal
```

- 🌱 Thế là xong rồi, giờ mình chỉ cần set-url remote theo tên Host đã config thôi là chạy phà phà rồi.

```sh
git@github.com:anhnh-3008/app.git -> git@git-personal:anhnh-3008/app.git
```

- 🌱 Ngoài ra trong file .gitconfig còn có thể setup được cả color branch, alias, editor, ... Mình có chôm được mấy cái [settings](https://github.com/ttuan/dotfiles/blob/master/git/gitconfig) hay hay của một anh ở công ty, mọi người có thể tham khảo nhé =)) nếu thấy hay thì cho anh mình một ⭐ nha <3
