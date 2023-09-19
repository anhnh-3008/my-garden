---
title: "🔐 Single Sign-On(SSO)"
tags: [til, sys Design]
date: 2022-09-27
---

## 🌿  Issue
Hiện nay hầu hết các dịch vụ web đều yêu cầu người dùng đăng nhập trước khi sử dụng. Nhu cầu sử dụng dịch vụ ngày càng nhiều đồng nghĩa chúng ta càng phải nhớ nhiều thông tin đăng nhập, giả sử nếu chúng ta dùng 10 webs khác nhau, việc nhớ thông tin đăng nhập cũng khá là 'vất vả' đúng ko nào =))
- Chính vì vậy mà đã lòi ra cu SSO này =))

## 🌿  What?
![[00 Meta/01 Attachments/Single Sign-On.png]]

- `Single Sign-On` là cơ chế giúp người dùng đăng nhập một ID cho một vài trang webs hoặc hệ thống liên quan nhưng độc lập với nhau. Kiểu như Google dùng tài khoản Gmail đăng nhập cho các services độc lập(Driver, Clouds, ...). Một khóa mở được nhiều chìa 🤞

## 🌿  Why?
### Ưu điểm
- Giảm thời gian nhập lại thông tin đăng nhập
- Giảm [password fatigue](https://en.wikipedia.org/wiki/Password_fatigue) cho hệ thống
- Giảm effort phát triển chức năng log-in
- Giảm thiểu rủi ro việc lộ thông tin của người dùng
- Nâng cao hiệu suất cho người dùng. Người dùng ko phải nhớ nhiều thông tin đăng nhập.
- Quản lý dễ dàng hơn. Giả sử bạn có 3 trang webs và bạn muốn ban account A, nếu dùng SSO bn chỉ cần setting banned một lần cho cả 3 webs.

### Nhược điểm:
- Phụ thuộc vào bên thứ 3


🌱 Lắm ưu ít nhược nên SSO khá là ngon, hiện tại cũng có khá nhiều service thứ 3 cung cấp dịch vụ SSO miễn phí(Facebook, Google, Github, ...) mọi người có thể cân nhắc sử dụng theo nhu cầu phát triển của dự án nhé =))

## 🌿  How?
SSO là một phần của [[50 til/51 Code/08 System Design/System Identification Link]], có liên quan chặt chẽ với việc xác thực thông tin người dùng. Nó sẽ định danh người dùng, và sau đó chia sẻ thông tin định danh được với các hệ thống con.

### Cơ chế
Theo luồng bình thường user đăng nhập web A sẽ sinh ra cookie để xác thực cho những request sau, nếu mang cookie đó sang web B để xác thực thì sẽ tạch do các trình duyệt hiện nay chỉ có thể truy cập cookie do chính nó tạo ra.
![[00 Meta/01 Attachments/Auth SSO.png]]
Hiểu đơn giản giữa các web sẽ có một **browser cookie storage** chung và sử dụng cơ chế Cross-origin resource sharing. Khi Web nào đăng nhập thì sẽ truy cập vào **browser cookie storage** để lấy cookie lên **server auth**(của bên thứ 3) để xác thực.

