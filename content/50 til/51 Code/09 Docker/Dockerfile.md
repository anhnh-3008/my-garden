---
title: "🐬 Dockerfile"
tags: [til, docker]
date: 2022-09-21
aliases: [dockerfile]
---


## 🌿 I. Config

- **FROM**: chỉ định image gốc. [[50 til/51 Code/09 Docker/Docker]] Hub nơi lưu trữ và chia sẻ các images. Chúng ta có thể lấy các image gốc trên này và về xào nấu lại để phù hợp với nhu cầu sử dụng của mình.

- **MAINTAINER**: optional để đặt tên cho tác giả viết Dockerfile

- **RUN**: thực thi 1 câu lệnh trong quá trình build image.

- **CMD**: thực thi 1 câu lệnh trong quá trình bật [[50 til/51 Code/09 Docker/Docker|container]].

	- Mỗi **Dockerfile** chỉ chạy một câu lệnh CMD, nếu có nhiều hơn sẽ chỉ chạy câu lệnh **CMD** cuối cùng.
	
	- Nếu muốn khởi động nhiều ứng dụng khi start container, hay sử dụng **ENTRYPOINT**.

- **ENTRYPOINT**: thực thi một số câu lệnh trong quá trình bật container, những câu lệnh này sẽ được viết trong file script có đuôi .sh.

- **EXPOSE**: chỉ định cổng mà container sẽ nghe khi chạy.

- **ADD**: Copy file, thư mục, hoặc remote file thêm chúng vào filesystem của image.

- **COPY**: Copy file, thư mục từ host machine vào image. Có thể sử dụng url cho tập tin cần copy(chưa dùng baoh =))).

- **WORKDIR**: chỉ định directory cho câu lệnh CMD

- **VOLUME**: mount thư mục từ máy host vào container.


Mình sẽ build những gì học được về docker ở repo này : [app-demo-rails-docker]( https://github.com/anhnh-3008/app-demo-rails-docker), mọi người có thể theo dõi các steps theo pulls cho tiện nhé. 

Pull mình build Dockerfile: [pull build Dockerfile](https://github.com/anhnh-3008/app-demo-rails-docker/pull/1)
