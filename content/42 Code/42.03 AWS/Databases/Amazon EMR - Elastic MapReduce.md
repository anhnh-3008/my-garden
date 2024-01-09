---
title: "🌱 Amazon EMR - Elastic MapReduce"
tags: [aws]
date: 2023-04-05
alias: [emr]
---

## 🌿 What?
- Là dịch vụ hỗ trợ quản lý các clusters Hadoop(Big Data) để phân tích và triển khai các ứng dụng big data.
- Clusters có thể được tạo bởi hàng trăm EC2 instances.
- EMR nó take care hết toàn bộ các tài nguyên cung cấp cũng như thông số thiết lập.
- Tự động scale và tích hợp với Spot instances.
- Use case: data processing, ML, web indexing, big data, ...

## 🌿 Node types
- **Master Node:** quản lý cluster, điều phối, quản lý sức khỏe - chạy dài hạn.
- **Core Node:** Chạy các tasks và lưu trữ dữ liệu - chạy dài hạn.
- **Task Node(optional):** chỉ để chạy task - thường là Spot.

## 🌿 Purchasing
- On-demand: tin cậy, có thể dự tính, sẽ không bị terminated.
- Reserved(min là1 năm): tiết kiệm chi phí(EMR sẽ tự động sử dụng option này nếu nó phù hợp)
- Spot instances: rẻ hơn nhưng có thể bị terminated nếu được giá =)) kém độ uy tín.

