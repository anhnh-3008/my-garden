---
title: "🐬 Docker"
tags: [post, docker]
date: 2022-09-20
aliases: [docker, docker-compose, container, docker commands]
---

---

## I. Bối cảnh
---

**![](https://lh6.googleusercontent.com/l1T2krPv068MLPC1J8jYFIDgQ47_VT1VmUcFofBWypN-Kb-EX6IBfULvpeD4TsBh40meAUN-7A6erjR-s48nkuQxA8xWOxAC4GiFLLWPoyLHEViSScy14ABVJP0VPY8sT1MMUFNDBp8yTOQWxEZcgS0erEK4qO9orhKcrRJEv_6KlyPbbjl-Pmca)**
🌱 Trước đây mô hình máy chủ được tạo thành bởi ba yếu tố:
* Máy chủ vật lý (Physical Server)
- Hệ điều hành ([[50 til/51 Code/51.03 Operating System/Linux Basic|Operating System]])
- Các ứng dụng (Application)

Mô hình trên có những nhược điểm:
-   Một máy chủ chỉ cài được 1 OS
-   Cho dù ổ cứng khủng, ram khủng thì cũng không thể tận dụng hết được

🌱 Vì những nhược điểm đó, công nghệ ảo hóa **Virtualization** được ra đời, ưu điểm so với mô hình cũ là:
-   Trên một máy chủ vật lý, có thể cài được nhiều hệ điều hành, tận dụng được tài nguyên tốt hơn do có thể phân chia tài nguyên cho từng máy ảo

Nhưng vẫn có những thứ chưa được tối ưu:
-   Về tài nguyên:
	-   Khi thiết lập máy ảo chúng ta sẽ cần cấu hình để cung cấp tài nguyên từ ổ cứng và ram từ máy thật cho máy ảo. Những tài nguyên được phân ra sẽ là cố định. Dẫn đến việc, khi bật máy ảo, kể cả khi không làm gì thì máy thật cũng sẽ mất một lượng tài nguyên mà ban đầu chúng ta đã cung cấp.
-   Về thời gian:
	-   Thời gian bật/tắt máy ảo khá lâu(mấy phút lận)

🌱 Để khắc phục những nhược điểm còn tồn đọng đó, công nghệ **Containerization**, ưu điểm của công nghệ này đó là:

![](https://lh4.googleusercontent.com/mUbQaVuvrz58iy4ySacviA8nGD1-MNeX6TzY3sSxY982frJtmsICy3JZplo52qHH4ffyiy01eKZpH9x0oE2nMgnkLT7l2iAHkSzoucvthQsozcYFAt1soJAmHPjftBXcQ8x5EGPJYzYV5GvZJ9LTZ1XfFTvNzMf8K6wBMei84RzAicKTG0fBsVLk)

-   Thừa hưởng khả năng tạo được nhiều máy ảo trên cùng một máy chủ vật lý như **Virtualization** , nhưng tốt hơn ở chỗ những máy ảo này sẽ dùng chung phần nhân và cùng chia sẻ với nhau tài nguyên của máy mẹ. Máy ảo dùng bao nhiêu tài nguyên sẽ được cấp bấy nhiêu, chứ ko có tình trạng tài nguyên bị rảnh rỗi nữa, như vậy thì việc tận dụng tài nguyên sẽ tối ưu hơn.
-   Đặc trưng của công nghệ này là sử dụng các **containers**.    

![](https://lh6.googleusercontent.com/r4-OlfYsbR1dZ0M_NkB6e49MefZWZUR2RZK2kppihpj1PTkebxA_C-cT4SIRJuKiNuSBYxpWO46t_-U16KCSHJNiYD9P1Mdr1SEIomyw9fi5gEga5srvhymPoJoOpx_sOtR2KJsytnhTDk6fhS-3O-7yfFuRPy5Oh6Tsi48i-BYiU999MuwBsSZ7)


🌱 Với công nghệ **Virtualization**, chúng ta có thể dùng các công cụ tiêu biểu như **Virtualbox** hay **VMware**, còn với **Containerization** đó chính **Docker**.

![](https://lh3.googleusercontent.com/tc5QldwzU46Kx0zuTQZ8inuJax19jfTODrl5z6Wo8KnYXExUbuEA1hKcQ6Os6R_RWv9qU0knCYzlFdOspkgtuE7LRgqrKEYqwdSfXOh7dCw1l3-7RYuKg6BqN_X22_JcGxJNA2Z1NFmMwEqI8mjspbvD6X8XWj7S86edsc-s269_XqNFF--EIkHb)


## II. What Docker?
---

- Là mã nguồn mở
- Mục đích develop, deploy and run applications bằng những containers

Xem hướng dẫn cài Docker tại [đây](https://docs.docker.com/engine/installation/)

## III. Why Docker?
---

- Build một lần dùng được nhiều lần và nhiều chỗ
- Bật/tắt nhanh chóng

## IV. Những khái niệm phổ biến
---

### 1. Container
---
- Là một quá trình chạy trên **[[50 til/51 Code/51.03 Operating System/Linux Basic|Linux kernel]]**. 
	Được cấp phát tài nguyên riêng: CPU, bộ nhớ và hệ thống tập tin. Chính vì vậy, Docker độc lập với những tiến trình đang chạy của máy tính và không ảnh hưởng đến các containers/processes khác đang chạy.

### 2. Image
---
Là tệp chứa mọi thứ cần để thực thi: dependencies, binaries, source code, ... Xây dựng bằng cách thực thi các câu lệnh trong **Dockerfile**. Một **Image** có thể được sử dụng để tạo nhiều **containers** giống nhau. Mỗi **container** là một **instantiation** của **image**.

### 3. Dockerfile
---
Là một tệp chứa các câu lệnh cần thiết để xây dựng một **Image**.

## V. Một vài câu lệnh hay được sử dụng
---

- **docker pull image_name**: pull một image từ Docker Hub.

- **docker build**: build một container từ Dockerfile và một context(bao gồm các folders|files được đặt ở PATH/URL).

- **docker run**: chạy container từ một image.

- **docker ps**: list ra những containers đang chạy. **-a/--all** để lấy tất cả containers hoặc -q/--quite nếu chỉ muốn lấy cấc ids của containers.

- **docker logs [container_id/container_name]**: xem logs của 1 container, **-f/--follow** để xem log output.

- **docker volume ls**: list ra các volumes được dùng để lưu trữ data được sinh ra và sử dụng bởi các containers.

- **docker rm [container_id/container_name]**: xóa 1 hoặc nhiều containers.

- **docker rmi [image_id]**: xóa 1 hoặc nhiều images.

- **docker stop**: dừng 1 hoặc nhiều containers.

- **docker kill**: kill 1 hoặc nhiều containers.

- **docker kill $(docker ps -q)**: kill tất cả containers đang chạy
```cmd
$(docker ps -q) #lấy ra id của các containers đang chạy.

$(docker ps -a -q) #lấy id của toàn bộ các containers.
```

- **docker system prune**: Dọn toàn bộ resources(images, containers, volumes, networks) đang bị treo(không liên kết với bất kì container nào).

