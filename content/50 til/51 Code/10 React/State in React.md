---
title: "🌱 State in React"
tags: [til, react]
date: 2023-06-26
alias: [state]
---

## 🌿 What?
- Là nơi lưu trữ dữ liệu được sử dụng chung cho các components trong React.
	- Nó cũng giống như một Global Variable, có thể sửa đổi giá trị ở bất kỳ file nào.

## 🌿 Why?
- Ví dụ chúng ta cần hiển thị tổng số lượng click vào các buttons.
![[00 Meta/01 Attachments/Pasted image 20230626111547.png]]

## 🌿 Identify
- Các đặc điểm không phải là State:
	- Biến không thay đổi theo thời gian.
	- Biến được truyền từ một parent thông qua [[50 til/51 Code/10 React/Props in React|props]].
	- Có thể tính toán được giá trị của biến dựa trên state đã có hoặc [[50 til/51 Code/10 React/Props in React|props]] trong component.