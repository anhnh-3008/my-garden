---
title: "🌱 Amazon FSx"
tags: [aws]
date: 2023-03-23
---

## 🌿 Overview
- Launch 3rd party - một file system có hiệu suất cao trên AWS.
- Dịch vụ toàn quyền quản lý.
- 4 loại phổ biến:
	- **FSx for Lustre**
	- **FSx for NetApp ONTAP**
	- **FSx Windows File Server**
	- **FSx for OpenZFS**

## 🌿 FSx for Windows File Server
- Quản lý hoàn toàn hệ thống file Windows.
- Hỗ trợ giao thức SMB và Windows NTFS.
- Tich hợp Microsoft Active Directory, ACLs, user quotas.
- Có thể mounted vào trong Linux EC2 Instances.
- Hỗ trợ **Microsoft's Distributed File System (DFS) Namespaces**(Nhóm các files trên nhiều FS).
- Storage options:
	- **SSD** - độ trễ thấp, tính toán nhanh(databases, media processing, data analytics, ...).
	- **HDD** - phù hợp để lưu trữ dữ liệu lớn, ít được truy cập hơn.
- Có thể truy cập từ những hạ tầng có sẵn(VPN chẳng hạn).
- Có thể config multi-AZ.
- Dữ liệu được backup hàng ngày vào S3.

## 🌿 FSx for Lustre
- Là một kiểu hệ thống files phân phối song song, dùng cho những trường hợp tính toán phức tạp
- Cái tên Lustre có nguồn gốc từ 'Linux' và 'cluster'
- Dùng cho ML, **High Performance Computing (HPC)**
- Storage options:
	- **SSD**
	- **HDD**
- Có khả năng tích hợp liền mạch với S3
	- Có thể đọc S3 như một file system(thông qua FSx)
	- Có thể ghi ngược vào S3( thông qua FSx)
- Có thể sử dụng từ những hệ thống sẵn có của mình(VPN chẳng hạn)

### 🍃 Deployment Options
- **Scratch File System**
	- Lưu trữ tạm thời
	- Dữ liệu không được nhân bản
	- Nhanh gấp 6 lần option kia
	- Usage: sử dụng với những tiến trình ngắn hạn, tối ưu giá tiền
- **Persistent File System**
	- Lưu trữ lâu
	- Dữ liệu được nhân bản trong AZ
	- Thay thế file lỗi trong vài phút
	- Usage: sử dụng với những tiến trình dài hạn, với những dữ liệu nhạy cảm

## 🌿 FSx for NetApp ONTAP
![[00 Meta/01 Attachments/Pasted image 20230323221704.png]]
- Quản lý NetApp ONTAP trên AWS
- **Tương thích với các giao thức NFS, SMB, iSCSI**.
- **Có thể clone dữ liệu tại bất kỳ thời điểm nào.**

## 🌿 FSx for OpenZFS
![[00 Meta/01 Attachments/Pasted image 20230323221840.png]]
- Quản lý OpenZFS trên AWS
- **Có thể clone dữ liệu tại bất kỳ thời điểm nào.**