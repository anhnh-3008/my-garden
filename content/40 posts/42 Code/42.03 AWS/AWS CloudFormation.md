---
title: "🌱 AWS CloudFormation"
tags: [aws]
date: 2023-04-27
alias: [cloudformation]
---

## 🌿 What?
- Là một bản phác thảo cho kiến trúc hạ tầng trên AWS, cho hầu hết các resources trên AWS.
- Ví dụ, chúng ta cần một kiến trúc bao gồm:
	- Security Group
	- 2 EC2 Instances sử dụng SG trên
	- Một [[40 posts/42 Code/42.03 AWS/S3|S3]] Bucket
	- Một ELB
- CloudFormation sẽ tạo tất cả **theo đúng trình tự** như trên và **đúng theo những thông số mà chúng ta đã chỉ định**.

## 🌿 Benefits
- **Infrastructure as code** 
	- Không phải tạo resources thủ công nữa.
	- Các thay đổi về resources sẽ được review thông qua code.
- Chi phí:
	- Dễ dàng theo dõi chi phí theo stack build trong code.
	- Có thể ước lượng được chi phí sử dụng nhờ CloudFormation template.
	- Saving strategies: ở môi trường dev, có thể dễ dàng tự động xoá template vào lúc 6 giờ chiều(khi mn tan làm) và bật lại vào lúc 8 giờ sáng(khi mọi người bắt đầu làm việc).
- Hiệu suất:
	- Có khả năng xoá, tự động tạo infrastructure ở bất cứ đâu.
	- Tự động tạo biểu đồ cho template
	- Lập trình khai báo(không cần thực hiện theo thứ tự, vd như cần tạo một [[40 posts/42 Code/42.03 AWS/Databases/Amazon DynamoDB|DynamoDB]] thì phải tạo trước một EC2 Instance, ... CloudFormation tự tìm được cách thực hiện)
- Không chế tạo lại bánh xe(tận dụng những cái có sẵn)
	- Tận dụng những templates sẵn có trên web.
	- Tận dụng lại các tài liệu.
- **Hỗ trợ hầu như tất cả các AWS resources**
	- Có thể sử dụng "custome resources" cho những resources không được hỗ trợ.

## 🌿 Stack Designer
![[00 Meta/01 Attachments/Pasted image 20230427110235.png]]
- Chúng ta có thể thấy được **toàn bộ resouces** được áp dụng cho infrastructure.
- Ngoài ra còn có thể thấy được **quan hệ** của chúng.