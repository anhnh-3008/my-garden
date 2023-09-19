---
title: "⚙️ Config SSH"
tags: [til, ssh]
date: 2022-09-29
---

## 🌿 Issue
- 🌱Chắc hẳn là một dev BE, các bạn ít nhiều cũng từng có lần ssh lên server để check log, xem db, hay là config dự án, ... Quy trình đểcó thể ssh được lên  server sẽ gồm có những bước cơ bản như sau:
	- Tạo một bộ khóa tại máy local.
	- Đưa public key cho bên infra hoặc người có thể lên được server, để họ thêm key của chúng ta vào 1 file - file này sẽ chứa các keys có thể ssh.
- 🌱 Sau đó mỗi lần ssh chúng ta sẽ cần phải gõ command:

```sh
ssh user_name@ip
```

- 🌱 Vấn đề ở đây là, chúng ta khó có thể nhớ chính xác 2 thông tin trên cho mỗi lần ssh. Trước đây mình sẽ note những thông tin này vào một chỗ nào đấy bí mật, khi nào cần ssh thì bật lên và copy vào, rất là mất thời gian. Đã thế khi gen ra nhiều key ssh, mình còn phải set -i để chỉ định ssh-key nào sẽ được dùng để ssh nữa.

## 🌿 Solution

- 🌱 Khi search vấn đề này, mình thấy mọi người thường sẽ không dùng cách stupid trên kia của mình mà sẽ sử dụng file  ~/.ssh/config. Và nó giải quyết hoàn toàn được 2 vấn đề mình gặp phải ở trên.
	1. Không cần nhớ thông tin ssh: user_name, ip
	2. Không cần chỉ định bằng cơm ssh-key khi ssh nữa
- 🌱 Mọi người chỉ cần thêm vào file ~/.ssh/config như ở dưới:

```sh
Host project-dev
  Hostname 1.0.5.374
  User deployer
  IdentityFile ~/.ssh/project-dev-ecdsa

Host project-prod
  HostName 1.12.6.52
  User deployer
  IdentityFile ~/.ssh/project-pro-ecdsa
```

- Host: tên tắt dùng để ssh, có thể đặt tên theo project để dễ nhớ nhé. 
- Hostname: ip server
- User: user trên server
- IndentityFile: chỉ định ssh-key sẽ dùng để ssh cho Host

🌱 Việc đơn giản bây giờ là chúng ta ssh theo Host thôi 💪🏻 !!

```sh
ssh project-dev
```
