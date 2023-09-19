---
title: "🐬 Docker Network"
tags: [til, docker]
date: 2022-09-21
aliases: [docker, network]
---

## 🌿 What? 

🌱 Là mạng sử dụng cho các **containers** có thể kết nối và giao tiếp với nhau. Mỗi **container** có một vùng chứa riêng biệt nên cũng sẽ có mạng, port, IP riêng.

🌱 **[[50 til/51 Code/09 Docker/Docker]]** cung cấp sẵn một số mạng mặc định cho các **container**, chúng ta có thể gom một nhóm **[[50 til/51 Code/09 Docker/Docker|container]]** vào một mạng chung. Điều này khá là tiện lợi trong trường hợp chúng ta muốn chỉ định một stack phù hợp cho dự án.

## 🌿 What type of network?

- 🌱 Bridge network
	- Mạng **Bridge** cho phép kết nối giữa các **container** cùng mạng và sử dụng một dải ip được cấp ngẫu nhiên hoặc tự thiết lập.
	- Mạng Bridge đáp ứng hầu hết các usecase nếu triển khai các container trên cùng một host. Nhưng nếu chạy một môi trường đa host, **Bridge** sẽ không làm được điều này, đây sẽ là nhược điểm của mạng **Bridge**.
	- Driver của mạng **Bridge** là **bridge**.

- 🌱 Host network
	- **Host network** cho phép mạng **container** kết nối với **host**. Và sử dụng IP có cùng dải mạng với **host**.
	- Driver của mạng **Host** là **host**.

- 🌱  None network
	-   Tắt tất cả kết nối mạng.
	-   Driver của mạng **None** là **null**.

- 🌱  Overlay network
	-   Nhược điểm của mạng **Bridge** được **Overlay network** và **Macvlan** khắc phục.
	-   **Overlay network** thực hiện kết nối nhiều **Docker daemon** với nhau để tạo một mạng ảo trên các máy chủ. Nơi có thể thiết lập kêt nối giữa **swarm service** và **container** độc lặp hoặc hai **container** trên các host khác nhau.
	-   Driver của mạng **Overlay** là **overlay**.

- 🌱  Macvlan netwrok
	-  **Macvlan network** cho phép bạn gán địa chỉ MAC cho một **container**, biến **container** như một thiết bị vật lý trên mạng.
	-   Driver của mạng **Macvlan** là **macvlan**.

