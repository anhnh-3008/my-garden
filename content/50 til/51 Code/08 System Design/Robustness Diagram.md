---
title: "🌱 Robustness Diagram"
tags: [til, sys design]
date: 2022-10-24
---

## 🌿 What?
- 🌱 Là một dạng UML diagram nằm trong `ICONIX Process`, xác định tất cả những objects và mối liên hệ của từng `use case`.
	- Giảm sự mơ hồ của phần mô tả `use case`, dễ dàng hơn cho việc thiết kế, kiểm tra và estimate. 

![[00 Meta/01 Attachments/01.02 TIL/18 System Design/Robustness Diagram/Robustness reponsibility.excalidraw.png]]

> [!info] ICONIX Process
> 
> `ICONIX Process` là một phương pháp luận phát triển phần mềm, mục tiêu là để tránh [analysis paralysis](https://en.wikipedia.org/wiki/Analysis_paralysis). Chỉ sử dụng 4 UML cơ bản ứng với 4 bước trong quá trình chuyển đổi từ `Use Case text` thành `Code` .

- 🌱 Mỗi diagram sẽ trả lời cho từng câu hỏi:
	- `Use Cases` - Users đang làm gì?
	- `Domain Models` - Có những Objects nào?
	- `Robustness Diagrams` - Những Object nào tham gia trong từng `use case`?
	- `Sequence Diagrams` - Những Object tương tác với nhau như thế nào?

## 🌿 How?
- 🌱 Sử dụng khuôn mẫu `boundary/control/entity class`.

- 🌱 4 nguyên tắc cơ bản:
	- `Actors` chỉ có thể giao tiếp với `Boundary objects`.
	- `Boundary objects` chỉ có thể giao tiếp với `Control objects` hoặc `Actors`.
	- `Entity objects` chỉ giao tiếp được với `Control objects`.
	- `Control objects` có thể giao tiếp với `Boundary objects`, `Entity objects` và một số `Control objects` khác, nhưng cấm chơi với `Actors`.
> [Ý nghĩ của các khuôn mẫu](https://docs.nomagic.com/display/MD190/Robustness+diagram#:~:text=Boundary%20or%20Interface,and%20entity%20objects.)

![[00 Meta/01 Attachments/01.02 TIL/18 System Design/Robustness Diagram/Object Rubustness.excalidraw.png|500]]


- 🌱 Ví dụ:

![[00 Meta/01 Attachments/01.02 TIL/18 System Design/Robustness Diagram/Robustness of use case access to homepage.excalidraw.png]]

## 🌿 Tham khảo
- https://en.wikipedia.org/wiki/ICONIX
- https://docs.nomagic.com/display/MD190/Robustness+diagram