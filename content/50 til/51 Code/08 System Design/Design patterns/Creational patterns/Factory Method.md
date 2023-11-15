---
title: 🌱 Factory Method
tags:
  - til
  - design-patterns
date: 2023-10-25
aliases:
  - factory method
draft: false
---
# 🌿 What?
Factory Method là pattern cung cấp một interface cho việc khởi tạo object trong superclass nhưng cho phép các subclasses có thể thay đổi được kiểu của object tạo ra.

Nghe rất đớ 🥴🥴🥴

Factory Method ra đời để giải quyết vấn đề Open/Close Principles trong [[50 til/51 Code/01 Style/SOLID|SOLID]]. Giúp hệ thống có thể dễ dàng mở rộng hoặc loại bỏ code một cách dễ dàng, ít bị ảnh hưởng đến base.

# 🌿 Problem
Khái niệm đọc hơi khó hiểu những ví dụ sẽ trực quan hơn và chắc là mọi người cũng đã sử dụng rồi nhưng không biết tên thôi.

Ví dụ chúng ta cần viết một Hệ thống quản lý Vận tải.

![[00 Meta/01 Attachments/Pasted image 20231025155022.png]]

Ban đầu, hệ thống chỉ mới áp dụng cho vận tải xe tải(truck). Code của hệ thống sẽ được ốp hết ở trong class Truck.
![[00 Meta/01 Attachments/Pasted image 20231025155341.png|center]]
Vấn đề xảy ra khi hệ thống mở rộng, giờ cần xử lý thêm cả vận tải trên biển bằng tàu nữa(ship). Giờ sửa là phải sửa lại một đống code base để check object xem là loại đi Ship 🚢 hay loại đi Truck 🚚.

# 🌿 Solution
Ý tưởng của Factory Method có thể hiểu như tính trừu tượng trong OOP, thiết kế ra những phần chung để tái sử dụng và mở rộng.

![[00 Meta/01 Attachments/Pasted image 20231025160141.png]]

Như ví dụ trên hệ thống cần xử lý thêm vận chuyển bằng Tàu. Có thể sửa lại base của hệ thống như sau:
- Tạo class Logistics định nghĩa những phương thức dùng chung như planDelivery() và **phương thức chung nhưng có cách thức hoạt động riêng - Abstract function**
	- Ví dụ như Con Chó và Con Chó Sói đều có phương thức chung là Kêu nhưng một con Kêu gâu gâu, một con Kêu Chu Chu 😅
- Tạo class RoadLogistics và SeaLogistics cho từng loại hình vận tải, cả 2 class đều kế thừa class Logistics. Chịu trách nhiệm tạo ra các object vận chuyển(Tàu, Xe Tải)

![[00 Meta/01 Attachments/Pasted image 20231025160148.png]]
- Interface sẽ định nghĩa ra những method chung cho các object vận chuyển(Tàu, Xe Tải) ví dụ như move() và deliver(). Các class implement interface sẽ có trách nhiệm định nghĩa chi tiết các methods trên phù hợp theo Class.

=> Theo mô hình này thì có mở rộng ra thêm AirLogistics(máy bay, tên lửa) hoặc bỏ RoadLogistics đi thì cũng không ảnh hưởng gì đến những phần đã có sẵn
# 🌿 References
- https://refactoring.guru/design-patterns/factory-method
