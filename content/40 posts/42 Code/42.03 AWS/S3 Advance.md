---
title: "🌱 S3 Advance"
tags: [aws]
date: 2023-03-15
---

## 🌿 Lifecycle Rules
- Có thể chuyển các objects giữa các storage classesclassescác.
- Ví dụ với những object ít được truy cập thường xuyên, cho nó vào **Standard IA**
- Với những object cần lưu trữ, không cần tốc độ truy cập cao, chuyển nó vào **Glacier or Glacier Deep Archive**
- Việc chuyển các objects có thể thực hiện tự động bằng một **LifeCycle Rules**.
- Có 2 actions chính:
	- **Transition Actions:** thiệt lập các điều kiện để chuyển object sang store class khác.
		- vd move objects sang Standard IA class sau 60 ngày từ ngày khởi tạo.
		- move objects sang Glacier sau 6 tháng
	- **Expiration actions:** thiết lập thời hạn cho objects.
		- Có thể thiết lập xoá sau 365 ngày
		- **Có thể sử dụng để xoá old versions(nếu versioning được bật)** 
		- Có thể dùng để xoá những object chưa hoàn thành khi thực hiện Multi-Part uploads.
- Rules có thể tạo cho một certain prefix, ex: s3://mybucket/mp3/*
- Rules cũng có thể tạo cho certain objects Tags, ex: Department Finance

## 🌿 Requester Pays
- Mặc định, người dùng sở hữu buckets sẽ phải trả phí cho cả việc lưu trữ cũng như phí băng thông khi có người tải dữ liệu từ buckets.
![[00 Meta/01 Attachments/Pasted image 20230315112349.png]]

- Tuy nhiên, chúng ta có những tập dữ liệu lớn và có những người dùng muốn tải xuống để phục vụ nhu cầu cá nhân chẳng hạn, chúng ta không cần lo phần phí **networking** kia, chúng ta có thể lựa chọn option **requester pays**.
![[00 Meta/01 Attachments/Pasted image 20230315112541.png]]
- Khi bật tính năng này, user muốn download resources thì cần phải authen với AWS, để AWS còn tính bill cho phí **networking**.

## 🌿 Event Notifications
![[00 Meta/01 Attachments/Pasted image 20230315134320.png]]
- Là những thông báo được gửi đến các destinations(SNS, SQS, Lambda Function) khi có một sự kiện gì đó tác động đến bucket(created , removed, restore, replication, ...)
- Có thể filter các event, ví dụ như chỉ cần nhận thông báo các sự kiện trigger đến object có đuôi là *.jpg* chẳng hạn.
- **Có thể tạo số lượng S3 events tuỳ thích**
- Thường các thông báo sẽ được truyền đi trong vài giây, nhưng cũng có thể thỉnh thoảng sẽ mất vài phút hoặc lâu hơn.

- Ngoài 3 destinations nhận event notifications, Amazon có thêm một tính năng mới, một destination cho event notifications, đó là **Amazon EventBridge**.

### 🍃 Amazon EventBridge
![[00 Meta/01 Attachments/Pasted image 20230315135039.png]]

- Giờ là tất cả các các thông báo event đi qua **cái cầu** này trước, sau đó đi đâu thì sẽ được quyết định theo các rules.
- Ưu điểm:
	- **Advanced filtering** - có thể filter theo điều kiện phức tạp hơn(metadata, object size, name, ...)
	- **Multiple Destinations** - có thể điều hướng event notifications tới nhiều điểm đến hơn.
	- **Capabilities** - Cung cấp khả năng lưu trữ, lặp lại sự kiện, truyền tải uy tín hơn.

## 🌿 Baseline Performance
- Amazon [[40 posts/42 Code/42.03 AWS/S3|S3]] sẽ tự động scales để đáp ứng nhu cầu sử dụng tối thiểu(tỉ lệ requests cao, độ trễ thấp 100-200ms)
- App của bạn có thể đạt được ít nhất **3,500 PUT/COPY/POST/DELETE hoặc 5,500 GET/HEAD requests / mỗi giây / mỗi prefix trong một bucket.**
- Điều đó có nghĩa nếu chúng ta đồng thời đọc 4 prefixs, sẽ có thể đạt được 22,000 GET/HEAD requests / mỗi giây / mỗi prefix trong một bucket.

## 🌿 Performance
![[00 Meta/01 Attachments/Pasted image 20230315142907.png]]
- Làm sao để upload một cách tối ưu?
	- **Multi-Part upload:**
		- recommended nên sử dụng cho những files > 100MB, bắt buộc phải dùng cho những file > 5GB
		- Tính năng này sẽ chia file lớn ra thành nhiều phần sau đó upload đồng thời các phần, lên [[40 posts/42 Code/42.03 AWS/S3|S3]] thì sẽ tự động ghép lại thành một files như ban đầu.
- Làm thế nào để tranfer một file một cách tối ưu?
	- **S3 Transfer Acceleration**
		- Tăng tốc độ truyền file bằng một AWS edge location, nó giúp gia tốc quá trình truyền file đến một region chỉ định.
		- Giảm thiểu dữ liệu truyền trên public network, sử dụng mạng private của AWS như kiểu đi xe ở làn ưu tiên, thoáng với nhanh hơn.
		- Có tương thích với tính năng **Multi-Part**
- Làm thế nào để đọc file một cách tối ưu?
	- **S3 Byte-Range Fetches**
		- Thực hiện đồng thời các câu GETS cho từ byte ranges.
		- Có khả năng phục hồi tốt hơn khi request thất bại(bởi gì chia ra làm các phần nên đọc lại cũng nhanh hơn)
		- Có thể sử dụng để download nhanh hơn
		- Có thể sử dụng để hiển thị một phần thông tin cùa file, vd như phần đầu file để biết trước nội dung là gì chẳng hạn.
![[00 Meta/01 Attachments/Pasted image 20230315143732.png]]

## 🌿 Batch Operations
- Thao tác đồng thời với nhiều dữ liệu bằng một request.
	- Sửa metadata, properties
	- **Mã hoá hoặc giải mã objects**
	- ...
- Chức năng cung cấp viêc quản lý progress, thông báo gửi thành công, tạo report, ...
- **Bạn có thể sử dụng S3 Inventory để lấy danh sách object và sử dụng S3 Select để filter đống objects đó.**
