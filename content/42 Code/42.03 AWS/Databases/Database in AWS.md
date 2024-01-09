---
title: "🌱 Database in AWS"
tags: [aws]
date: 2023-04-04
---

## 🌿 Types
- **RDBMS(=SQL/OLTP):** [[42 Code/42.03 AWS/Databases/Amazon RDS - Relational Database Service|RDS]], [[42 Code/42.03 AWS/Databases/Amazon Aurora|Aurora]].
- **NoSQL:** [[42 Code/42.03 AWS/Databases/Amazon DynamoDB|DynamoDB]](~JSON), [[42 Code/42.03 AWS/Databases/Amazon ElastiCache|ElastiCache]] (key/value), Neptune(graphs),DocumentDB(MongoDB), Keyspaces(Apache Cassandra).
- **Object Store:** [[42 Code/42.03 AWS/S3|S3]](cho những object lớn) / Glacier(backup/archives).
- **Data Warehouse:** Redshift(OLAP), Athena, EMR.
- **Search:** OpenSearch - free text, tìm kiếm phi cấu trúc.
- **Graphs:** Amazon Neptune - hiển thị quan hệ của dữ liệu.
- **Ledger:** Amazon Quantum Ledger Database.
- **Time series:** Amazon Timestream.

## 🌿 Amazon RDS - Summary
- Tóm tắt ý chính của [[42 Code/42.03 AWS/Databases/Amazon RDS - Relational Database Service|RDS]]:
	- Hỗ trợ với PosgreSQL / MySQL / Oracle / SQL Server / MariaDB / Custom
	- Cung cấp RDS Instance Size và [[42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]] Volume Type & Size
	- Có khả năng tự động scale cho Storage
	- Hỗ trợ Read Replicas và Mutil AZs
	- Bảo mật với IAM, SG, KMS, SSL in transit.
	- Tính năng Automated Backup với từng thời điểm(tối đa lưu trữ trong 35 ngày)
	- Tính năng Manual DB Snapshot giúp lưu trữ với thời gian dài.
	- Hỗ trợ Xác thực IAM, tích hợp với Secrets Manager
	- RDS Custom có thể dùng để truy cập và customize các instance cơ bản(Oracle & SQL Server)
	- **Use cases**: dùng khi muốn lưu trữ cơ sở dữ liệu có quan hệ, thực hiện các câu lệnh SQL, các transactions.

## 🌿 Amazon Aurora - Summary
- Tóm tắt ý chính của [[42 Code/42.03 AWS/Databases/Amazon Aurora|Aurora]]:
	- Tương thích với PostgreSQL / MySQL, tách biệt giữa lưu trữ và tính toán.
	- Storage: Dữ liệu được lưu trữ trong 6 replicas trên 3 AZ - vì vậy nó luôn HA, tự động khôi phục nếu có lỗi, tự động scale.
	- Compute: Các cụm DB instance nằm trên nhiều AZ, tự động scale với Read Replicas.
	- Cluster: Custom endpoint cho các DB instances đọc và ghi.
	- Về bảo mật / monitoring / bảo trì / backup giống với RDS.
	- **Aurora Serverless:** dùng khi không dự đoán trước được nhu cầu sử dụng.
	- **Aurora Multi-Master:** liên tục ghi dữ liệu(luôn dự phòng, khả năng ghi luôn sẵn sàng).
	- **Aurora Global:** Lên đến 16 DB read instances trên từng region, < 1 giây để nhân bản
	- **Aurora Machine Learning:** dùng với ML sử dụng module SageMaker & Comprehend trên Aurora.
	- **Aurora Database cloning:** Một cụm mới được clone từ cụm đã tồn tại, nhanh hơn sử dụng snapshot để restoring.
	- **Use Cases:** giống với nhu cầu sử dụng RDS, nhưng yêu cầu cần nhanh hơn, ít cần bảo trì hơn, linh hoạt hơn, hiệu suât tốt hơn và nhiều tính năng khác nữa.

## 🌿 Amazon ElastiCache - Summary
- Tóm tắt ý chính của [[42 Code/42.03 AWS/Databases/Amazon ElastiCache|ElastiCache]]:
	- Được quản lý bởi Redis hoặc Memcached(giống như RDS nhưng dùng cho cache)
	- Lưu dữ liệu trong bộ nhớ tạm, độ trễ cực thấp
	- Phải cung cấp một  EC2 instance.
	- Hỗ trợ Clustering(redis) và Multi AZ, Read Replicas
	- Bảo mật thông qua IAM, SG, KMS, Redis Auth
	- Backup / Snapshot / Lưu trữ tại thời điểm chỉ định.
	- Quản lý và lập lịch cho bảo trì.
	- **Yêu cầu phải thay đổi code của app để sử dụng**
	- **Use Cases:** Lưu trữ dạng Key/Value, dữ liệu cần đọc thường xuyên, ít ghi, cache các kết quả của các câu SQL queries, lưu phiên hoạt động của websites, không thể sử dụng SQL.

## 🌿 Amazon DynamoDB - Summary
- Tóm tắt ý chính của [[42 Code/42.03 AWS/Databases/Amazon DynamoDB|DynamoDB]]:
	- Công nghệ độc quyền của AWS, là database NoSQL serverless, độ trễ milisecond.
	- Capacity modes:
		- Optional auto-scaling: chủ động setting các thông số khi có plan cũng như ước lượng được trước nhu cầu sử dụng.
		- On-demand: không ước lượng được trước, nó sẽ tự động scale theo mức độ sử dụng của mình, dùng đến đâu trả đến đấy.
	- Có thể thay thế ElastiCache để lưu trữ dạng key/value
	- DAX cluster cache kết quả đọc, giảm độ trễ cũng như giảm số lượng truy cập đến DB.
	- Bảo mật, xác thực, phân quyền thông qua IAM.
	- Event processcing: DynamoDB Streams để tích hợp với AWS Lambda hoặc Kinesis Data Streams.
	- Global Table: thiết lập nhiều DB cùng active, dữ liệu được đồng bộ với nhau.
	- Tự động backup tối đa 35 ngày với PITR(để lưu trữ 1 bảng mới) hoặc on-demand backups.
	- **Nhanh chóng phát triển**
	- **Use case:** Phát triển ứng dụng với kiến trúc serverless, phân phối cache không máy chủ.

## 🌿 Amazon S3 - Summary
- Tóm tắt ý chính của [[42 Code/42.03 AWS/S3|S3]]:
	- S3 là là một dạng lưu key/value cho các objects
	- Phù hợp với những objects lớn, không phù hợp với nhiều objects nhỏ.
	- Serverless, scale vô hạn, size của object tối đa là 5TB, có khả năng quản lý version.
	- **Tiers:** S3 Standard, S3 Infrequent Access, S3 Intelligent, S3 Glacier + lifecycle policy.
	- **Features:** Versioning, Encryption, Replication, MFA-Delte, Access Logs, ..
	- **Security:** IAM, Bucket Policies, ACL, Access Points, Object Lambda, CORS, Object/Vault lock
	- **Batch operation:** trên các objects sử dụng S3 Batch, liệt kê các files thì sử dụng S3 Inventory.
	- **Performance:** Multi-Part upload, S3 Transfer Acceleration, S3 Select.
	- **Automation:** S3 Event Notifications(SNS, SQS, Lambda, EventBridge)
	- **Use case:** Static files, key/value objects lưu trữ với những objects lớn, website hosting.

## 🌿 DocumentDB - Summary
- Tóm tắt ý chính của DocumentDB:
	- Là Aurora nhưng tương thích với mongoDB
	- Sử dụng để lưu trữ, query và index dữ liệu JSON.
	- Toàn quyền quản lý, HA với các nhân bản trên cả 3 AZ.
	- Tự động phát triển 10Gb - 64Tb,
	- Tự động scale worloads lên đến hàng triệu requests.

## 🌿 Amazon Neptune - Summary
- Graph database
- Một ứng dụng phổ biến là **social network**.
- HA trên 3 AZ, tối đa mở rộng 15 read replicas.
- Build và chạy các apps hoạt động với các bộ dữ liệu có kết nối phức tạp - Nó đã được tối ưu với những queries khó và phức tạp.
- Có thể lưu trữ lên đến hàng tỷ quan hệ và query với độ trễ cực thấp(milisecond)

## 🌿 Amazon KeySpaces  - Summary
*Apache Cassandra là một database open-source NoSQL*
- Tương thích với Apache Cassandra.
- Serverless, có thể scale, HA, toàn quyền quản lý bởi AWS.
- Tự động scale các bảng dựa theo lượng sử dụng của app.
- Các bảng sẽ được nhân bản ba lần trên nhiều AZ.
- Sử dụng Cassandra Query Language(CQL)
- Mode: on-demand và provisioned mode.
- Encryption, backup, Point-In-Time Recovery(PITR) tối đa 35 ngày.
- Use case: lưu trữ thông tin thiết bị IoT, time-series data, ...

## 🌿 Amazon QLDB  - Summary
- Quantum Ledger Database.
- Là một cái sổ cái để **lưu lại các giao dịch tài chính**.
- Toàn quyền quản lý, serverless, HA, Nhân bản trên cả 3 AZ.
- Sử dụng để **review lại lịch sử của toàn bộ những thay đổi đối với dữ liệu của app** từ trước đến nay,
- **immutable system:** không tác nhân nào có thể xóa, sửa.

## 🌿 Amazon Timestream  - Summary
- Nhanh, có thể scale, **serveless database time series.**
- Tự động scale để điều chỉnh khả năng sử dụng.
- Lưu trữ và phân tích hàng nghìn tỷ events mỗi ngày.
- Rẻ nhất
- Use case: IoT apps, phân tích real-time, ...