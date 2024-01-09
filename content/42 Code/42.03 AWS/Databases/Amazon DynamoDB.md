---
title: "🌱 Amazon DynamoDB"
tags: [aws]
date: 2023-03-28
alias: [dynamodb]
---

## 🌿 What?
- Là dịch vụ cung cấp cơ sở dữ liệu toàn quyền quản lý, HA(Highly available) với khả năng nhân bản trên nhiều AZs.
- Kiểu NoSQL - không phải kiểu quan hệ. Hỗ trợ transaction.
- Có khả năng scale với những dự án lớn.
- Chịu được hàng triệu requests mỗi giây, hàng triệu triệu hàng, và hàng trăm TB dung lượng.
- Hiệu suất nhanh và nhất quán.
- Tích hợp được với IAM để bảo mật, phân quyền và quản trị viên.
- Chi phí thấp và có khả năng tự động scaling
- Không bảo trì hay vá version, vì AWS luôn cung cấp sẵn infrastructure nên không cần lo.
- Có 2 loại bảng trong DynamoDB:
	- Standard Table
	- Infrequent Access(IA) Table

## 🌿 Basics
- DynamoDB được tạo thành từ các **bảng**.
- Từng bảng có mọt **Primary Key** được chỉ định từ lúc khởi tạo.
- Từng bảng có thể có vô hạn các item(các hàng).
- Từng item có các **attributes**(có thể thêm bất kỳ lúc nào - có thể null)
- Một item có size tối đa là **400KB**
- Các kiểu dữ liệu được hỗ trợ:
	- **Scalar Types:** String, Number, Binary, Boolean, Null.
	- **Document Types:** List, Map.
	- **Set Types:** String Set, Number Set, Binary Set.
- **Vì vậy, DynamoDB có thể giúp chúng ta phát triển nhanh chóng.**

## 🌿 Read/Write Capacity Modes
- Kiểm soát thông lượng. Có 2 mode:
- **Provisioned Mode(default)**
	- Có thể chỉ định số lượng reads/writes trên mỗi giây
	- Bạn cần có một plan về khả năng sử dụng trước.
	- Trả cho Read Capacity Units (RCU) & Write Capacity Units (WCU)
	- Có thể add auto-scaling cho RCU và WCU
- **On-Demand Mode**
	- Read/write tự động được scale theo khả năng sử dụng.
	- Không cần phải lên kế hoạch sử dụng trước.
	- Dùng đến đâu, trả đến đấy - đắt hơn cái trên
	- Phù hợp với những app không dự đoán trước được khả năng sử dụng, hoặc các app thử nghiệm, có thời gian sử dụng không dài.


