---
title: "🌱 Amazon SNS - Simple Notification Service"
tags: [aws]
date: 2023-03-25
alias: [sns]
---

## 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20230325164033.png]]
- Giống với [[40 posts/42 Code/42.03 AWS/Amazon SQS - Simple Queue Service|SQS]], nhưng cái này theo mô hình publish/subcriber. 
- Phù hợp khi ứng dụng có mô hình một service gửi message tới một số services được chỉ định.

- Mỗi topic có thể set được 12,5000,000 subs.
- Giới hạn 100,000 topics.
- Các subcribers có thể nhận notification từ SNS:
![[00 Meta/01 Attachments/Pasted image 20230325164534.png]]

- Nhiều AWS Services có thể gửi dữ liệu trực tiếp đến SNS:
![[00 Meta/01 Attachments/Pasted image 20230325164723.png]]

## 🌿 Security
- Same [[40 posts/42 Code/42.03 AWS/Amazon SQS - Simple Queue Service|SQS]] security

## 🌿 SNS + SQS: Fan Out Pattern
![[00 Meta/01 Attachments/Pasted image 20230325205522.png]]
- Ý tưởng là muốn một message được gửi tới nhiều Queues.
- Gửi noti vào SNS, setup các subcribers là các Queues.
- Hoàn toàn tách biệt, không bị mất dữ liệu.
- Có thể thêm nhiêu Queues hơn về sau.
- Phải setup access policy cho phép SNS ghi vào SQS.
- Cross-Region Delivery: họat động với cả những Queues khác region.

## 🌿 FIFO Topic
- Giống với bên [[40 posts/42 Code/42.03 AWS/Amazon SQS - Simple Queue Service|SQS]].
- Nếu set Topic là FIFO thì chỉ có thể nhận SQS FIFO queues là subcribers.

## 🌿 Message Filtering
![[00 Meta/01 Attachments/Pasted image 20230325211312.png]]
- Như một lớp filter theo điều kiện để các Queue nhận message từ SNS.
- Nếu không có filter, Queue sẽ nhận được tất cả các messages từ SNS.
