---
title: "🌱 CNAME and Alias"
tags: [aws]
date: 2023-03-11
---

## 🌿 What?
- Cả 2 đều là loại bản ghi DNS của Route53.
- CNAME:
	- Ánh xạ một tên miền cho một tên miền khác.
	- Chỉ dùng được cho **NON-ROOT DOMAIN**.
- Alias:
	- Ánh xạ một tên miền tới các AWS Resource(ELB, CloudFront, ...)
	- Dùng được cho cả **ROOT DOMAIN** và **NON ROOT DOMAIN**.
	- Không phải trả phí.
	- Có sẵn health check.

## 🌿 Alias Records
- Ánh xạ domain tới một AWS resource.
- Một extension
- Tự động nhận ra các thay đổi đối với địa chỉ IP của các resources.
- Không như CNAME, có thể sử dụng với top node của DNS namespace(Zone Apex)
- Luôn luôn là kiểu A/ AAAA đối với các AWS Resources
- Không thể thiết lập TTL, nó sẽ được Route53 tự động set.

## 🌿 Targets
![[00 Meta/01 Attachments/Pasted image 20230311160422.png]]
- **Không thể set Alias Record cho một EC2 DNS**

