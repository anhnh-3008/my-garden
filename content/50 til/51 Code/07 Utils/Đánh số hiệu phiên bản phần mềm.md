---
title: "🌿 Đánh số hiệu phiên bản phần mềm"
tags: [til]
date: 2022-11-09
---

### 🌿 What?  
- 🌱 Là quy tắc để xác định và phân biệt tên của phần mềm ở mỗi giai đoạn phát triển. 
- 🌱 Sematic Versioning  
	- Là quy tắc thường được sử dụng nhất. Do [Tom Preston-Werner](https://tom.preston-werner.com/) (ng sáng lập và là cựu CEO của Github) tạo ra.
	- Có format là `[major].[minor].[patch]` , vd: 5.6.8
		-   `major`  - tăng lên khi có những thay đổi **không tương thích với phiên bản cũ** (vd thay đổi cấu trúcc response).
		-   `minor`  - tăng lên khi thêm tính năng mới **nhưng vẫn tương thích với phiên bản cũ** (vd thêm trường trả về trong response).
		-   `patch`  - tăng lên khi fix bug **nhưng vẫn tương thích với phiên bản cũ**.

### 🌿 Refer
[https://viblo.asia/p/semantic-versioning-OeVKBN2EKkW](https://viblo.asia/p/semantic-versioning-OeVKBN2EKkW)