---
title: "🌱 Best practice when build Dockerfile"
tags: [til, docker]
date: 2023-01-03
---

## 🌿 I. Chỉ định rõ version của Base Image

- 🌱 Bad

```Dockerfile
FROM ruby
...
```

- 🌱 Good

```Dockerfile
FROM ruby:3.1.2
...
```

- Nên chỉ định rõ version để có thể tái sử dụng. Cũng tiện theo dõi khi chúng ta muốn upgrade & maintain. 

## 🌿 II. Chỉ nên sử dụng trusted or official base images

- 🌱 Bad

```Dockerfile
FROM random-dude-on-the-internet/ruby:3.1.2
```

- 🌱 Good

```Dockerfile
FROM ruby:3.1.2

# hoặc 

FROM random-dude-on-the-internet/ruby:3.1.2

# giả sử chúng ta biết chắc rằng random-dude-on-the-internet uy tín/tín.
```

- Vì chúng ta không thể chắc rằng Base Image có được sửa đổi hay không. Với những nguồn không uy tín, nếu người viết không ghi change log rõ ràng có thể gây ảnh hưởng đến hệ thống.

## 🌿 III. Chỉ định rõ version của dependencies

- 🌱 Bad

```Dockerfile
FROM ruby:3.1.2

RUN gem install sinatra
```

- 🌱 Good

```Dockerfile
FROM ruby:3.1.2

RUN gem install sinatra -v 2.0.5
```

- Tương tự như base image, chúng ta cũng nên chỉ định rõ version cho dependencies. Hầu hết các trình quản lý package như `Gemfile.lock`, `package-lock.json`, `yarn.lock` đều chỉ định rõ, dễ dàng quản lý, theo dõi cũng như thuận tiện tái sử dụng.

## 🌿 IV. Đưa những commands ít thay đổi lên trước  

- 🌱 Bad

```Dockerfile
FROM ruby:3.1.2

# Source code
COPY my-code/ /srv/

# Application dependencies
COPY Gemfile Gemfile.lock ./
RUN bundle install
```

- 🌱 Good

```Dockerfile
FROM ruby:3.1.2

# Application dependencies
COPY Gemfile Gemfile.lock ./
RUN bundle install

# Source code
COPY my-code/ /srv/
```

- Docker sẽ build lại tuần tự từ trên xuống dưới, bắt đầu từ câu lệnh có 'thay đổi'. Ví dụ như trên, source code sẽ được thay đổi thường xuyên hơn Gemfile, nếu đặt source code ở trên, Docker sẽ build lại cả phần `COPY` với `RUN bundle install` nữa. 

> [!note] Note 
> 
> Đặt các lệnh ít có khả năng thay đổi nhất ở trên cùng để tận dụng cache, giảm thời gian build Image.

## 🌿 V. Tránh chạy container với quyền root

- 🌱 Bad

```Dockerfile
FROM ruby:3.1.2

RUN gem install sinatra -v 2.0.5

RUN echo 'require "sinatra"; run Sinatra::Application.run!' > config.ru

# By default this is run as root
CMD rackup
```

- 🌱 Good

```Dockerfile
FROM ruby:3.1.2

RUN gem install sinatra -v 2.0.5

# Tạo user riêng để chạy container
RUN adduser -D my-sinatra-user

# Chỉ định User thực hiện các câu lệnh RUN, CMD hoặc ENTRYPOINT ở dưới
USER my-sinatra-user

# Chỉ định thư mục riêng
WORKDIR /home/my-sinatra-user

RUN echo 'require "sinatra"; run Sinatra::Application.run!' > config.ru

# Các câu lệnh sẽ chạy với quyền của user my-sinatra-user
CMD rackup
```

- Mặc định container run với quyền root.
- Container của chúng ta sẽ tạo ra một process chạy với quyền root trong Linux kernel, điều này có thể gây ra lỗ hổng bảo mật, cho phép attackers thoát khỏi container và thực hiện quyền root trên thiết bị của chúng ta.

## 🌿 VI. Sử dụng -chown khi run COPY hoặc ADD

- 🌱 Bad

```Dockerfile
FROM ruby:3.1.2

# Tạo user riêng để chạy container
RUN adduser -D my-sinatra-user

# Chỉ định User thực hiện các câu lệnh RUN, CMD hoặc ENTRYPOINT ở dưới
USER my-sinatra-user

# Chỉ định thư mục riêng
WORKDIR /home/my-sinatra-user

# File copy sẽ thuộc sở hữu của root user
COPY Gemfile Gemfile.lock ./

RUN bundle install

CMD rackup
```

- 🌱 Good

```Dockerfile
FROM ruby:3.1.2

# Tạo user riêng để chạy container
RUN adduser -D my-sinatra-user

# Chỉ định User thực hiện các câu lệnh RUN, CMD hoặc ENTRYPOINT ở dưới
USER my-sinatra-user

# Chỉ định thư mục riêng
WORKDIR /home/my-sinatra-user

# File copy sẽ thuộc sở hữu của my-sinatra-user user
COPY --chown=my-sinatra-user Gemfile Gemfile.lock ./

RUN bundle install

CMD rackup
```

- `USER` chỉ chỉ định user thực hiện `RUN`, `CMD` hoặc `ENTRYPOINT`. Còn với `COPY` và `ADD` chúng ta cần sử dụng `--chown`.

## 🌿 VII. Tránh làm lộ thông tin nhạy cảm trong Dockerfile

- 🌱 Bad

```Dockerfile
FROM ruby:3.1.2

ENV DB_PASSWORD "real password"
```

- Các thông tin như trên không bao giờ được hiện diện trong Dockerfile của chúng ta dưới dạng text thô. Thay vào đó, chúng ta có thể sử dụng thông qua những cách sau:
	- Lệnh `ARG` và truyền giá trị thông qua flag `--build-arg` khi run.
	- Biến môi trường.

> [!warning] Lưu ý
> Hai cách trên vẫn có rủi ro vì các giá trị thô sẽ vẫn được ghi lại trong lịch sử build.

## 🌿 VIII. Xóa luôn những thông tin nhạy cảm sử dụng để build

- 🌱 Bad

```Dockerfile
FROM ruby:3.1.2

ARG PRIVATE_SSH_KEY

# Bước này sẽ lưu lại PRIVATE_SSH_KEY
RUN echo "${PRIVATE_SSH_KEY}" > /root/.ssh/id_rsa

# Đến bước này vẫn sẽ còn giá trị của PRIVATE_SSH_KEY
RUN bundle install

RUN rm /root/.ssh/id_rsa
```

- 🌱 Good

``` Dockerfile
FROM ruby:3.1.2

ARG PRIVATE_SSH_KEY

RUN echo "${PRIVATE_SSH_KEY}" > /root/.ssh/id_rsa && \
  bundle install && \
  rm /root/.ssh/id_rsa
```

- Nếu có ai truy cập được vào lịch sử build thì có thể lấy được giá trị của PRIVATE_SSH_KEY. Chúng ta nên xóa luôn trong cùng một step để tránh trường hợp trên.

## 🌿 IX. Tối ưu size của base image nếu có thể

- 🌱 Bad

```Dockerfile 
FROM ruby:3.1.2

CMD ruby -e "puts 1 + 2"
```

- 🌱 Good

```Dockerfile 
FROM ruby:3.1.2-alpine

CMD ruby -e "puts 1 + 2"
```

- Base Image có nhiều version(chủ yếu khác nhau về base OS), chúng ta nên lựa chọn phù hợp với nhu cầu sử dụng. Mọi người có thể xem thêm ở [[50 til/51 Code/09 Docker/What is mean the tag suffix of an image on docker hub|đây]]
- Khi lựa chọn Image base từ OS thu gọn, cần để ý:
	- Phải có package manager và các gói có sẵn.
	- Xem OS đó sử dụng Shell gì.
	- Tránh các môi trường thử nghiệm, dễ gây rủi ro về mặt bảo mật hoặc tính ổn định.
