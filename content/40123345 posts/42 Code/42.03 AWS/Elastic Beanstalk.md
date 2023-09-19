---
title: "🌱 Elastic Beanstalk"
tags: [aws]
date: 2023-03-12
alias: [s3]
---


- Trên thực tế, một kiến trúc có thể áp dụng được cho rất nhiều các dự án hoăc một dự án có nhiều môi trường(dev, test, stg, production, ...). Mà mỗi dự án lại phải lọ mọ setup lại từng cái một (ELB, ASG, RDS, ElastiCache, ...) thì rất là một mỏi. Những lúc thế này, hãy nghĩ ngay tới **Elastic Beanstalk**.

## 🌿 What?
- **Elastic Beanstalk** sẽ tạo ra một môi trường giúp chúng ta thực hiện triển khai, mở rộng cho dự án. Chúng ta chỉ cần quan tâm đên source code phát triển tính năng của sản phẩm thôi.
- Nó sử dụng toàn bộ các components mà chúng ta đã sử dụng: ELB, RDS, ASG, ...
- Quan trọng là chúng ta vẫn có toàn quyền can thiệp vào quá trình config.
- Beanstalk thì miễn phí còn các dịch vụ nó quản lý bên trong(EC2 Instance, ELB, ...) thì chúng ta phải trả tiền như bình thường.

## 🌿 Components
- **Application**: Tổng hợp toàn bộ các component của một Beanstalk(enviroments, configuration, versions, ...)
- **Application Version**
- **Environments**
	- Tổng hợp toàn bộ AWS resourecs để chạy một website(chỉ chạy được mỗi ứng dụng một môi trường)
	- **Tiers**- quản lý từng tầng, vd như tầng server và tầng worker.
	- Có thể tạo nhiều enviroments(test, dev, stg, production)

![[00 Meta/01 Attachments/Pasted image 20230312233517.png]]

## 🌿 Deployment modes
- **Single Instance**
![[00 Meta/01 Attachments/Pasted image 20230312233803.png]]

- **High Availability**
![[00 Meta/01 Attachments/Pasted image 20230312233815.png]]

