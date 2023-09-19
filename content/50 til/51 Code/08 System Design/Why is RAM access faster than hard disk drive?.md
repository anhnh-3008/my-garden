---
title: "♻️ Why is RAM access faster than hard disk drive?"
tags: [til, sys design]
date: 2022-10-06
---

Khi sử dụng Redis, mọi người thường hay nói Redis thực hiện thao tác dữ liệu trên Ram nên có tốc độ truy xuất nhanh hơn rất nhiều so với truy cập vào HDD. Vậy tại sao lại như thế? 
 
## 🌿 Why?

![[00 Meta/01 Attachments/Communication between CPU - RAM - Hard Storage.png]]


- HDD nằm cách xa CPU, được kết nối với bảng điều khiển thông qua cổng SATA. 6Gb/s là tốc độ tiêu chuẩn của SATA III, HDD chỉ có thể đọc hoặc viết chứ không thể làm cả hai trong cùng một thời điểm.
- RAM nằm rất gần CPU và có kết nối băng thông rất cao. Thông lượng của DDR4 là khoản 40Gb/s, ngoài ra RAM còn có thể thực hiện đọc và viết cùng lúc. Khi sử dụng dual channel, RAM sẽ đọc/đọc, viết/đọc, viết/viết chính vì vậy mà nó có thể thao tác một lượng dữ liệu vô cùng lớn trong cùng một thời điểm.


## 🌿 Câu hỏi
Thế tại sao người ta lại không thiết kế để HDD lại gần CPU?
Vấn đề lớn nhất là chi phí. Tốc độ xử lý cao tương ứng với giá thành sản xuất cũng sẽ đắt. Và tùy theo mục đích nên mỗi phần sẽ có thiết kế phù hợp -> đạt được cả hiệu năng và giá thành tốt nhất.
-   Đối với những tác vụ lưu trữ file, đọc/ ghi đơn giản, không yêu cầu xử lý nhanh thì người ta dùng HDD cho rẻ. (ổ cứng lưu trữ)
-   Các tác vụ cần xử lý nhanh hơn 1 chút, như load hệ điều hành, người ta ưu tiên dùng SSD (ổ cài win ý :v )
-   Thằng nào cần cache, xử lý tốc độ bàn thờ (làm bộ nhớ tạm cho các phần mềm đang chạy) thì người ta dùng tới RAM, CPU.

![[00 Meta/01 Attachments/Why is RAM access faster than hard disk drive acess.png]]
