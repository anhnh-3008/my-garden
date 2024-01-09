---
title: "🌱 Amazon Route 53"
tags: [aws]
date: 2023-03-09
---

## 🌿 What?
- Dịch vụ cung cấp tính khả dụng cao, khả năng mở rộng cũng như quản lý DNS.
- Route 53 là một Domain Registrar.
- Có khả năng check the health của các resources
- Service duy nhất của AWS cung cấp 100% availability SLA.
- Tại sao lại là số 53? 53 là cổng của DNS.

## 🌿 Records
- Định nghĩa cách mà bạn muốn điều hướng traffic cho một domain
- Một record chứa:
	- **Domain/SubDomain name** - vd: example.com
	- **Record Type** - vd: A or AAAA
	- **Value** - 12.34.56.78
	- **Routing Policy** - Route 53 responds như thế nào
	- **TTL** - thời gian record được cached lại ở DNS Resolvers
- Route 53 hỗ trợ những kiểu DNS records sau:
	- must know: A/ AAAA / CNAME / NS
	- advance: CAA / DS / MX / NAPTR / PTR / SOA / TXT / SPF / SRV

### 🍃 Types
- A - maps một hostname với IpV4
- AAAA - maps một hostname với IpV6
- CNAME - maps một hostname với một hostname khác.
	- Mục tiêu phải là một record A hoặc AAAA
	- Không thể tạo một CNAM record là node đầu tiên của DNS, vd không thể đặt là example.com mà phải đặt là www.example.com
- NS - Name Servers cho Hosted Zone
	- Kiểm soát lượng truy cập được định tuyến đến một domain.

## 🌿 Hosted Zones
- Là khu vực chứa thông tin định tuyến lượng truy cập tới một domain
- **Public Hosted Zones** - chứa những records được chỉ định để định tuyến truy cập trên internet
- **Private Hosted Zones** - chứa những records được chỉ định để định tuyến truy cập trong một hoặc nhiều VPCs
- Phải trả 0.5 $ một tháng cho tính năng này.

## 🌿 Records TTL(Time to Live)
- Thời gian chỉ định để clien cache lại thông tin IP của DNS. Nếu TTL chưa hết hạn, khi client gọi lại Domain, sẽ truy cập vào địa chỉ IP đã truy cập lần đầu, kể cả chúng ta có thực hiện thay đổi IP cho DNS. Chỉ đến khi hết hạn TTL, thông tin IP mới mới được refresh.
- High TTL, 24h
	- Ít traffic tới Route 53
	- Có thể hết hạn records.
- Low TTL, 60s
	- Nhiều traffic tới Route 53(thêm $)
	- Hết hạn records trong thời gian ngắn hơn.
	- Dễ dàng thay đổi records.
- **Ngoại trừ Alias records, TTL là thông tin bắt buộc của mỗi một DNS record.**

