---
title: 🌱 Hướng tiếp cận refactor với một dự án mới
tags:
  - "#refactoring"
date: 2024-07-15
aliases: 
draft: false
---
> [!questions] Question
> Khi bạn muốn refactoring một đoạn code hay dự án mới tinh, bạn chưa biết gì về nghiệp vụ cũng như logic, bạn cần làm những gì để đảm bảo chất lượng và tính chính xác phần code mà bạn sẽ sửa đổi?

# I. 🔍 Tìm hiểu source code
- Tìm đọc tài liệu, hiểu được nghiệp vụ cơ bản và logic của dự án.
- Chạy và kiểm tra code

# II. 📝 Viết UnitTests
- Đảm bảo viết đầy đủ unit tests trước khi thực hiện refactor code.

> [!tip] Giúp hiểu được sâu logic code. Quan trọng hơn là sẽ đảm bảo phần refactor không ảnh hưởng đến logic hiện tại.

# III. 📏 Nắm rõ các nguyên tắc cơ bản
- Phần này tôi muốn đề cập đến các nguyên tắc của OOP và [[50 til/51 Code/01 Style/SOLID|SOLID]]
- Tư duy theo hướng xác định Objects, properties và methods.
	- Áp dụng 4 nguyên tắc của OOP.
		- Đóng gói
		- Trừu tượng
		- Kế thừa
		- Đa hình
- [[50 til/51 Code/08 System Design/Design patterns/Design patterns|Design patterns]]

# IV. 🏗️ Refactor Code
> [!note] Tiêu chí
> - Dễ đọc, dễ tiếp cận
> - Giảm sự phức tạp
> - Tái sử dụng
> - Dễ bảo trì
> - Dễ mở rộng
> - Cải thiện hiệu suất

Tùy theo yêu cầu của dự án, độ ưu tiên của các tiêu chí trên sẽ có sự thay đổi. Nhưng nếu không bị dí deadline quá thì chúng ta nên đảm bảo đầy đủ các tiêu chí này. Mà tính ra code clean thì thời gian phát triển, duy trì cũng như mở rộng về sau sẽ được giảm bớt, tốt nhất là nên chú trọng việc này ngay từ đầu 💪.
## 1. Dễ đọc, dễ tiếp cận
- Áp dụng lập trình hướng đối tượng OOP(đúng ra là OOP sẽ giải quyết được tất cả các tiêu chí ở trên, chắc chỉ trừ tiêu chí cải thiện hiệu suất 😄).
- Cải thiện tên biến và phương thức.
- Sử dụng convention chung(nếu có) hoặc thống nhất định dạng nhất quán. Ví dụ ưu tiên sử dụng early return, ...
- Tiêu chí này có bao quát tiêu chí Giảm sự phức tạp nữa.

## 2. Giảm sự phức tạp
-  DRY - loại bỏ code thừa, code trùng lặp.
- Tối ưu vòng lặp, các câu lệnh điều kiện.
- Giảm độ phức tạp của phương thức bằng cách tách logic thành các phương thức nhỏ hơn.

## 3. Tái sử dụng
- Tách mã nhỏ hơn.
- Áp dụng [[50 til/51 Code/08 System Design/Design patterns/Design patterns|design patterns.]]

## 4. Dễ bảo trì
- Đảm bảo tính đóng gói của OOP.
- Giảm sự phụ thuộc giữa các class hoặc module trong hệ thống, nên liên kết giữa các class thông qua abstract class. Thể hiện rõ ở nguyên tắc L(Liskov Substitution Principle) và D(Dependency Inversion Principle) trong [[50 til/51 Code/01 Style/SOLID|SOLID]] và tính trừu tượng trong OOP.

## 5. Dễ mở rộng
- Nguyên tắc S(Single Responsibility Principle) O(Open/Closed Principle) trong [[50 til/51 Code/01 Style/SOLID|SOLID]]. 
- Tính kế thừa và đa hình trong OOP.
- - Áp dụng [[50 til/51 Code/08 System Design/Design patterns/Design patterns|design patterns]].

## 6. Cải thiện hiệu suất
- Thuật toán.

# V. 📋 Kiểm tra và tài liệu hóa
- Kiểm tra lại mã theo bộ Unit tests đã viết ở bước 2.
- Cập nhật lại tài liệu để các thành viên trong dự án có thể nắm được các sửa đổi.