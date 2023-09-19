---
title: "🌱 Well-Architected Framework & Tools"
tags: [aws]
date: 2023-05-03
alias: [well architecture framework]
---

## 🌿 Well-Architected Framework
- Là tập hợp các nguyên tắc (best practice) để thực hiện việc build một kiến trúc trên AWS.
- Không dự đoán trước traffic của hệ thống, thay vào đó hãy sử dụng các service linh động hơn như [[40123345 posts/42 Code/42.03 AWS/ASG - Auto Scaling Group|ASG]].
- Nên thực hiện test hệ thống cả trên môi trường production, trên môi trường cloud việc này được hỗ trợ thực hiện dễ dàng và đảm bảo.
- Nên xây dựng để mọi người dễ tiếp cận với kiến trúc(phát triển, thay đổi, ...) vd như sử dụng [[40123345 posts/42 Code/42.03 AWS/AWS CloudFormation|CloudFormation]].
- Cho phép cải tiến kiến trúc. 
- Kiến trúc đảm bảo cho dữ liệu(đồng bộ, lưu trữ, ...)
- Luôn thử nghiệm để phát triển(vd như giả định tình huống flash sale cho app, xem kiến trúc có hoạt động tốt không)
- https://aws.amazon.com/architecture/well-architected

## 🌿 Six Pillars
![[00 Meta/01 Attachments/Pasted image 20230503205022.png]]
- Operational Excellent
- Reliability
- Security
- Performance Efficiency
- Cost Optimization
- Sustainability

-> Chúng ta không cần phải đánh đổi hay lựa chọn mức độ ưu tiên, tất cả sẽ liên kết và phụ thuộc lại để tổng hoà thành một hệ thống tốt.

## 🌿 Well-Architected Tool
- Là một công cụ miễn phí được giúp chúng ta review hệ thống dựa trên 6 trụ cột của Well-Architected Framework bằng cách trả lời các câu hỏi. Từ đó, công cụ này sẽ đưa ra những gợi ý để cải thiện hệ thống theo đúng chuẩn.