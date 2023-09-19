---
title: "🌱 The paradigms that generually applied when release"
tags: [til, deployment]
date: 2022-10-25
---


Với những dự án đã có cộng đồng người dùng lớn, việc deploy những tính năng mới lên môi trường `production` cần phải có những phương pháp để giảm thiểu tối đa những rủi ro cũng như đạt được trải nghiệm tốt nhất dành cho người dùng.  Những mô hình thường được áp dụng thực tế: `A/B Testing`, `Canary Deployments`  và  `Blue-Green Deployments`.

### 🌿 A/B Testing
- 🌱 Sử dụng để review độ hiệu quả và phản ứng của người dùng đối với những thay đổi mới.
- 🌱 Những thay đổi mới sẽ chỉ được `rolled out` với một bộ phận người dùng nhất định. So sánh đánh giá của người dùng để đưa ra những chiến lược phát triển phù hợp hơn trong tương lai.
- 🌱 Mô hình này được áp dụng cả cho phát triển web, bán hàng, quảng cáo, vv... 

![[00 Meta/01 Attachments/Pasted image 20221025184727.png]]


### 🌿 Blue-Green Deployments
- 🌱 Là một chiến lược deploy dùng để kiểm thử những tính năng mới của dự án.
- 🌱 Deploy without downtime.
- 🌱 Mô hình này gồm 2 servers chạy đồng thời là Blue và Green, đều là môi trường `production` nhưng một server có status `live` - nhận reqs của users còn server kia là `idle` - không hoạt động.

![[00 Meta/01 Attachments/Blue-Green Deployments.excalidraw.png]]

### 🌿 Canary Testing
- 🌱 Cũng giống 2 ý đầu của  `Blue-Green Deployments`.
- 🌱 Thay vì switch toàn bộ users truy cập giữa Blue và Green, `Canary Testing` sử dụng cân bằng tải, cho phép một số users có thể sử dụng version code mới, sau khi chạy ngon lành thì dần dần áp dụng cho toàn bộ users của hệ thống.

![[00 Meta/01 Attachments/Pasted image 20221025184522.png]]

### 🌿 Tham khảo
- https://www.oreilly.com/library/view/spring-50-microservices/9781787127685/6fab55ad-8897-42b7-b509-dd90850c861b.xhtml
- https://circleci.com/blog/canary-vs-blue-green-downtime/
