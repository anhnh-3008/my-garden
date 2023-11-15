---
title: 🌱Abstract Factory
tags:
  - til
  - design-patterns
date: 2023-10-25
aliases:
  - abstract factory
draft: false
---
# 🌿 What?
Abstract Factory có thể hiểu là pattern thiết kế cho những phần mang tính trừu tượng mà không cần chỉ ra những lớp cụ thể.
![[00 Meta/01 Attachments/Pasted image 20231025170913.png]]

# 🌿 Problem
Ví dụ chúng ta build một hệ thống giả lập cửa hàng nội thất. Trong đó có nhiều món đồ nội thất mang nhiều phong cách khác nhau.
![[00 Meta/01 Attachments/Pasted image 20231025164738.png]]

Giờ phải kiếm cách gì tạo ra được tất cả các nội thất và quan trọng khi thêm mới(nội thất hoặc phong cách) đều không ảnh hưởng đến code base.

# 🌿 Solution
Không cần quan tâm cụ thể hình thù của nội thất như thế nào, cứ thiết kết ra các interface liệt kê ra những phương thức chung của objects. Còn chi tiết thì sẽ được định nghĩa trong từng Class cụ thể.
![[00 Meta/01 Attachments/Pasted image 20231025171133.png]]

![[00 Meta/01 Attachments/Pasted image 20231025165321.png]]

# 🌿 References
- https://refactoring.guru/design-patterns/abstract-factory
