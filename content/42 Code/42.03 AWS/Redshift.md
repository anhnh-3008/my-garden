---
title: "🌱 Redshift"
tags: [aws]
date: 2023-04-05
alias: [redshift]
---

## 🌿 What?
- Là một data warehouse, cung cấp khả năng lưu trữ và phân tích lượng dữ liệu cực lớn.
- Base trên PostgreSQL **nhưng không sử dụng OLTP mà là OLAP - online analytical processing.**
- Hiệu suât tốt hơn x10 só với các data warehouses khác.
- Có thể scale từ một node tới hàng trăm nodes để đáp ứng nhu cầu sử dụng.
- Lưu trữ dữ liệu dạng cột thay vì hàng, có engine thực hiện query đồng thời.
- Trả phí dựa theo số lượng instances đã cung cấp.
- Có một giao diện SQL để thực hiện queries.
- Cung cấp các BI(business Intelligence) tools như Amazon Quicksight hoặc Taubleau.
- **vs [[42 Code/42.03 AWS/Databases/Amazon Athena|Athena]]:** truy vấn / joins / tổng hợp dữ liệu nhờ indexes nhanh hơn.

## 🌿 Cluster
- Leader node: để lên kế hoạch truy vấn, tổng hợp các dữ liệu.
- Compute node: để thực hiện truy vấn và gửi kết quả đến leader node.
- Bạn cân cung cấp node size.
- Có thể sử dụng Reserved Instances để tiết kiệm chi phí.
![[00 Meta/01 Attachments/Pasted image 20230405222056.png]]

## 🌿 Snapshots & DR
- Có thể tạo snapshot và ứng dụng như của [[42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]].
![[00 Meta/01 Attachments/Pasted image 20230405222723.png]]

## 🌿 Readshift Spectrum
![[00 Meta/01 Attachments/Pasted image 20230405223314.png]]

- Tăng khả năng xử lý phân tích dữ liệu cho [[42 Code/42.03 AWS/S3|S3]].
