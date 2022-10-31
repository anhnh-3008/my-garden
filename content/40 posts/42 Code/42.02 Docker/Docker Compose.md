---
title: "🦑 Docker Compose"
tags: [post, docker, docker-compose]
date: 2022-09-21
---

**![](https://lh6.googleusercontent.com/xSCCWpZ4m29JV6UPl9zCuNj4pDxdGD9shUACJ1auetH158BOcrCYKdtuETCxhgwHVjVrR4BFAeSCXAlz3-QfkhJ9tQoipVV2Taq0O64Bu_TITkvRfVM9io8uUNuc3Mf0amW_Z_mbRVEWhivppaEnymHpucB7YKB08UqkzUzYxoEp8SfG0pysEEpq-g)**

## I. What?
---

🌱 Chúng ta muốn ứng dụng [[40 posts/42 Code/42.02 Docker/Docker]] cho:
	- Dự án mới
	- Dự án đang phát triển

🌱 Chúng ta có thể dùng [[40 posts/42 Code/42.02 Docker/Dockerfile]] cài chung tất cả vào một container duy nhất sau đó chạy project trên container đó.
**![](https://lh4.googleusercontent.com/mS7LvI78YjVqb9jh1QY0K_KR_n_9jQJm_XLUhq-cVmKhgbj2KKqqA0xczpkSxfDPIf8Z85lI5J9-h1MDb2CLtR2Nod47XYNQFGtwwQ7qr0QqakS5hf9kGHoZ-05xQ46PG6vQI9z0RGCmfrTOe5HrezDmZkzdPnQY5yEMf28vQnubyKVXS0AcyTakDQ)**
🌱 Tuy nhiên cách này không hợp lý cho việc mở rộng cũng như sử dụng lại cho nhiều projects.
-> docker-compose ra đời để kết nối những containers riêng lẻ với nhau.
**![](https://lh5.googleusercontent.com/Jw9aHt8OVq5fMYhpOD_QYb0k3SGMT9hJvafVH7yiJdODYDeiQR_A6_b2wuXKhO5E5xr75B5wrl9KNL_jdRDgHHpiIvPCKxmZEToJ8_W1-C3vhRUGlAbfTHJHkfiBB6HKPSfWJEgqgawsqpFUa5h1WtDEVABZdKYvUCsO4f8VkXXMaXi12Hwff_xmNQ)**

---
- Có thể hiểu docker là con cá voi đang vận chuyển nhiều containers đến cảng Project A.
- Còn docker-compose sẽ là con bạch tuộc sử dụng các xúc tua của mình để lấy những containers cần thiết cho Project A.
---

Xem hướng dẫn cài docker-compose tại [đây](https://docs.docker.com/compose/install/)

## II. Xây dựng docker-compose
---

### 1. Cấu trúc thư mục
🌱 Mình sẽ chỉ làm một project demo nên cấu trúc đơn giản gồm:
- [x] docker/entrypoint.sh
- [x] Dockerfile
- [x] docker-compose.yml

🌱 Khi làm dự án thật, do phải build cho từng môi trường(development, staging, production) nên cấu trúc sẽ có khác hơn một chút, nhưng về cơ bản vẫn là vẫn có đủ thành phần cấu trúc như trên.

### 2. Xác định những containers cần thiết
🌱 Mình làm demo trên Rails app và những công nghệ mình thấy hay được sử dụng nhất là:
- [x] Web
	- Ruby
	- Rails(là Ruby framework nên chỉ cần pull image của ruby thôi)
- [x] Mysql (hoặc postgret)
- [x] Redis (lưu cache, backgournd job)
- [x] Sidekiq (chạy background job)

ok triển thôi!!

### 3. Viết docker-compose
1. **version**: những version sẽ có vài điểm khác nhau như:
	- về cấu trúc và các keys config
	- về Docker Engine version thấp nhất mà bạn cần đáp ứng
	- networking
Tại thời điểm viết bài này, trên trang chủ cập nhật version mới nhất là 3.8 hỗ trợ cho Docker Engine 19.03.0+
Chi tiết hơn về sự khác nhau của từng version hay các năng cấp từ 2.x lên 3.x thì mọi người có thể đọc thêm ở [đây](https://docs.docker.com/compose/compose-file/compose-versioning) nhé.
2. **services**: những containers chúng ta định nghĩa sẽ nằm ở đây.
3. những config trong từng container:
	- [x] **image**: chỉ định image được dùng để build container
	- [x] **build**: khi muốn build container bằng Dockerfile
	- [x] **container_name**: chỉ định tên tùy chỉnh của container nếu ko muốn dùng tên mặc định
	- [x] **restart**: mặc định là **no**, nếu set **always** container sẽ khởi động lại khi có lỗi
	- [x] **environment**: chỉ định biến mối trường, có thể chỉ định từng biến hoặc file chứa các biến môi trường
	- [x] **volumes**: chia sẻ dữ liệu từ máy ảo tới máy thật hoặc giữa nhiều containers với nhau
		- Ví dụ như container mysql, dữ liệu được tạo ra sẽ được lưu ở thư mục **var/lib/mysql**  trong container, nếu xóa container thì dữ liệu sẽ bị mất sạch.
		- Chính vì thế nên chúng ta dùng volumes để dữ liệu của container được mount ra ngoài host, nếu có xóa container thì dữ liệu vẫn còn, và khi khởi động lại, dữ liệu được mount ngược vào container và sử dụng bình thường.
	- [x] **ports**: Cấu hình cổng kết nối
		- có thể chỉ định cả 2 cổng **host:container** 
		- vd 123:345 cổng 123 của máy thật sẽ trỏ đến cổng 345 của container
