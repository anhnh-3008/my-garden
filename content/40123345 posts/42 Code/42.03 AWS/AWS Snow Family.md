---
title: "🌱 AWS Snow Family"
tags: [aws]
date: 2023-03-22
alias: [snow family]
---

## 🌿 What?
- Là dịch vụ có tính bảo mật cao, cung cấp các thiết bị di chuyển được dùng cho mục đích:
	- **Thu thập và xử lý dữ liệu trên các edge**
	- **Migrate data trong hoặc ngoài AWS**

- **Data migration:**
	- Snowcone
	- Snowball Edge
	- Snowmobile
![[00 Meta/01 Attachments/Pasted image 20230322210750.png]]

- **Edge computing:**
	- Snowcone
	- Snowball Edge
![[00 Meta/01 Attachments/Pasted image 20230322210759.png]]

## 🌿 Why?
- Lý do phải sử dụng Snow Family để chuyển dữ liệu vì thời gian truyền tải dữ liệu trên mạng là rất lâu.
![[00 Meta/01 Attachments/Pasted image 20230322211122.png]]

- Thử thách đưa ra cần giải quyết các vấn đề sau:
	- Kết nối bị giới hạn.
	- Băng thông cũng bị giới hạn.
	- Chi phí di chuyển cao.
	- Băng thông bị chia năm sẻ bảy(dùng chung -> không thể sử dụng tối đa được)
	- Kết nối ổn định(mạng public thì hay chập chờn)
- **Snow Family sẽ giải quyết các vấn đề trên bằng cách gửi thiết bị offline đến cho bn(qua bưu điện chẳng hạn), mất tầm khoảng một tuần, bạn nhận được và chỉ việc tải dữ liệu từ thiết bị offline lên AWS thôi.**
![[00 Meta/01 Attachments/Pasted image 20230322211904.png]]

## 🌿 Types

### 🍃 Snowball Edge
![[00 Meta/01 Attachments/Pasted image 20230322212938.png]]
- Giải pháp vật lý vận chuyển dữ liệu: move TBs hoặc PBs dữ liệu vào hoặc ra từ AWS, thay thế cho việc truyền tải dữ liệu qua mạng(và việc trả phí cho mạng)
- Trả tiền theo từng job
- Cung cấp block storage và Amazon S3-compatible object storage
- **Snowball Edge Storage Optimized**
	- Dung lượng HDD là 80TB
- **Snowball Edge Compute Optimized**
	- Dung lượng HDD là 42TB
- Use Cases: migrate cho dữ liệu lớn trên cloud, phục hồi sau thảm họa, ...

### 🍃 AWS Snowcone & Snowcone SSD
![[00 Meta/01 Attachments/Pasted image 20230322213729.png]]
- Nhỏ gọn, có thể thực hiện tính toán ở bất cứ đâu, bền bỉ và bảo mật, phù hợp với những môi trường cần dữ liệu không lớn.
- Nặng khoảng 2.1kg
- **Snowcone** - 8 TB HDD
- **Snowcone SSD** - 14 TB SSD
- Sử dụng khi Snowball không phù hợp(ví dụ như cần tối ưu cân nặng để mang lên máy bay chẳng hạn)
- Phải cung cấp sạc hoặc pin để nó hoạt động
- Có thể gửi về AWS offline hoặc connect nó với internet và sử dụng **AWS DataSync** để gửi dữ liệu.

### 🍃 AWS Snowmobile
![[00 Meta/01 Attachments/Pasted image 20230322213848.png]]

- Là một cái xe tải chở các thiết bị lưu trữ
- Dùng để vận chuyển dữ liệu lên đến exabyte(1EB = 1000PB = 1000000TBs)
- Mỗi một Snowmobile(1 xe tải) có dung lượng là 100PB
- Bảo mật cao, nhiệt được điều kiểm soát, GPS, video giáo sát 24/7
- Tối hơn Snowball nếu chúng ta muốn vận chuyển nhiều hơn 10PB dữ liệu.

## 🌿 AWS OpsHub
- Trước đây để sử dụng các thiết bị Snow Familly, bạn cần phải có 1 CLI tool
- Giờ chúng ta có thể sử dụng AWS OpsHub(một phần mềm có thể cài vào máy tính) để quản lý các thiết bị Snow Family.

## 🌿 Snowball into Glacier
- **Không thể chuyển dữ liệu trực tiếp từ Snowball vào Glacier được.**
- Chúng ta phải sử dụng Amazon S3 để nhận dữ liệu từ Snowball, sau đó kết hợp với S3 lifecycle police để chuyển dữ liệu vào Amazon Glacier.
![[00 Meta/01 Attachments/Pasted image 20230323213336.png]]

