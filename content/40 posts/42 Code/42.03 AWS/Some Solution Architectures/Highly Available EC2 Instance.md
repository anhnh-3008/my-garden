---
title: "🌱 Highly Available EC2 Instance"
tags: [aws]
date: 2023-04-24
alias: []
---

Một điều quan trọng cần lưu ý khi thiết kế hệ thống, đó là tính sẵn sàng cao, hệ thống luôn luôn sẵn sàng để truy cập, thời gian downtime hầu như là không có.

![[00 Meta/01 Attachments/Pasted image 20230424215507.png]]
- Sử dụng ElasticIP để gắn cho một EC2 Instance.
- Tạo một Standby EC2 Instance.
- Sử dụng [[40 posts/42 Code/42.03 AWS/Monitoring/Amazon CloudWatch|CloudWatch]] Event để theo dõi các thông số của EC2 Instance chính, nếu có nó có vấn đề gì bất thường(vd CPU nhảy lên 100% -> lỗi rồi) -> Gửi cho [[40 posts/42 Code/42.03 AWS/AWS Lambda|Lambda]] Function để thực hiện attach ElasticIP qua EC2 Instance. Thế là hệ thống đỡ mất thời gian để launch lại EC2 vì có sẵn rồi.

![[00 Meta/01 Attachments/Pasted image 20230424215827.png]]
- Sử dụng [[40 posts/42 Code/42.03 AWS/ASG - Auto Scaling Group|ASG]] để tự động mở rộng hệ thống tuỳ theo lưu lượng. Giảm khả năng bị quá tải của hệ thống.
- Có thể bật Multi-AZs, tránh khả năng datacenter đang sử dụng gặp sự cố.

![[00 Meta/01 Attachments/Pasted image 20230424220328.png]]
- Có một vấn đề là khi Terminate EC2 Instance, cả [[40 posts/42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]] Volume sẽ bị xoá theo, để có thể giữ lại nó, [[40 posts/42 Code/42.03 AWS/ASG - Auto Scaling Group|ASG]] sẽ sử dụng lifecycle hook, nó sẽ triggerd khi [[40 posts/42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]] Volume bị terminate -> tạo ra một [[40 posts/42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]] Snapshot, khi [[40 posts/42 Code/42.03 AWS/ASG - Auto Scaling Group|ASG]] launch một EC2 Instance mới, [[40 posts/42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]] cũng sẽ được tạo từ [[40 posts/42 Code/42.03 AWS/EBS Volume - Elastic Block Store|EBS]] Snapshot. Dữ liệu vẫn sẽ được giữ nguyên.
