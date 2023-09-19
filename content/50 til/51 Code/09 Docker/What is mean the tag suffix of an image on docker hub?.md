---
title: "🌱 What is mean the tag suffix of an image on docker hub?"
tags: [til, docker]
date: 2022-12-06
---

### 🌿 Vấn đề
- Khi chạy apt-get update , gặp lỗi KEYEXPIRED như dưới đây.

```sh
Step 3/15 : RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs vim cron
 ---> Running in 8437242de6eb
W: GPG error: http://deb.debian.org jessie-updates InRelease: The following signatures were invalid: KEYEXPIRED 1668891673
W: GPG error: http://deb.debian.org jessie Release: The following signatures were invalid: KEYEXPIRED 1668891673
```

### 🌿 Nguyên nhân
- Lỗi trên được xác định là do Dockerfile đang base theo Image `ruby:2.4.2` , sử dụng `debian:jessie` , đã hết hạn LTS.

> [!info] LTS (Long Term Time)
> 
> 🌱 [LTS (Long Term Support)]([https://wiki.debian.org/LTS](https://wiki.debian.org/LTS)) là một dự án hỗ trợ(cập nhật repo, vá lỗi, ...) các versions Debian ổn định đã được release trong vòng ít nhất là 5 năm. LTS không phải do Team Security Debian phát triển mà do một bộ phận những lập trình viên + công ty "tình nguyện" triển khai.

### 🌿 Giải pháp
Có 2 cách
1. 🌱 Sửa file `/etc/apt/sources.list`, replace repo `jessie-updates` bằng tay. Xem chi tiết hơn ở [đây](https://github.com/docker-library/ruby/issues/394).

 2. 🌱 Đổi Image `ruby:2.4.2 -> ruby:2.4.2-stretch`
	- Khi sử dụng Image, mọi người nên để ý phần tag xem nó đang được base theo version OS nào(nhất là các dự án thâm niên). Một số suffix thường gặp:
		- [-jessie](https://wiki.debian.org/DebianJessie) - Mã phát triển của Debian 8. Có LTS từ ngày 26/04/2015, hết hạn 30/06/2020.
		-  [-stretch](https://wiki.debian.org/DebianStretch) - Mã phát triển của Debian 9. Team Security Debian ngừng update bảo mật từ 06/07/2020 và đổi qua LTS -> đến khoảng 2025 là hết hạn LTS.
		-  [-buster](https://wiki.debian.org/DebianBuster) - Mã phát triển của Debian 10, released từ ngày 06/07/2019. Vẫn được Team Security Debian support.
		-  [-bullseyes](https://wiki.debian.org/DebianBullseye) - Mã phát triển của Debian 11, released từ ngày 14/08/2021. Vẫn được Team Security Debian support.
		- [-slim](https://github.com/docker-slim/docker-slim) - Tối ưu containers tốt hơn, nhỏ hơn, bảo mật hơn. Cân nhắc khi dùng, vì đây là phiên bản rút gọn, sẽ không đầy đủ bằng bản offical.
		- [-alpine](https://alpinelinux.org/) - Image được base theo Alpine Linux, đây là một OS thiết kế đặc biệt để chạy trong container. Có size rất bé, vài Mb(< slim). Highly recommended nếu bộ nhớ là tiêu chí ưu tiên. Xem thêm ở [đây](https://stschindler.medium.com/the-problem-with-docker-and-alpines-package-pinning-18346593e891).

### 🌿 Tham khảo
- Mọi người có thể đọc thêm những thông tin khác(bash, package management, ...) của các versions tag ở đây:
	- [https://stackoverflow.com/questions/52083380/in-docker-image-names-what-is-the-difference-between-alpine-jessie-stretch-an](https://stackoverflow.com/questions/52083380/in-docker-image-names-what-is-the-difference-between-alpine-jessie-stretch-an)