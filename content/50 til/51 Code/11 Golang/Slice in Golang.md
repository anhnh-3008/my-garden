---
title: "🌱 Slice in Golang"
tags: [golang]
date: 2023-06-27
alias: [slice]
---

## 🌿 Overview
- Trong Golang, độ dài của một array sẽ được coi là một phần của kiểu dữ liệu, vậy nên không thể thay đổi được.
```go
arr := [3]int{1,2,3} // arr có kiểu dữ liệu là [3]int
```

- Vì vậy, Golang cung cấp một thằng khác để giúp chúng ta sử dụng mảng thuận tiện hơn, đó là `slice`.

- Syntax khởi tạo giống với 1 array, nhưng không cần truyền độ dài, độ dài của `slice` sẽ bằng với số lượng phần tử khởi tạo.
``` go
slice := []int{1,2,3,4,5}
```

- Có thể khởi tạo một `slice` nil
```go
slice := []int{}
```

## 🌿 Slice mechanism
![[00 Meta/01 Attachments/Pasted image 20230627165733.png]]

- 🌱 Khởi tạo một `slice` , Go đồng thời sẽ tạo một `array` và trỏ con trỏ tới `array` đó.
- `slice` có 2 chỉ số cần quan tâm:
	- `length`: số lượng của các phần tử tồn tại trong `slice`
	- `capacity`: khả năng mở rộng của `slice`
![[00 Meta/01 Attachments/Pasted image 20230627170027.png]]

```go
// có thể khởi tạo 1 slice bằng func make
// 5 => capacity
// 3 => length
// length <= capacity, unless => error
slice := make([]int, 3, 5)

// length là số lượng ô nhớ có thể sử dụng luôn 
slice[0] = 1
slice[1] = 10
slice[2] = 20

slice[3] = 30 // => panic: runtime error: index out of range [3] with length 3
```

- 2 ô nhớ còn lại đã được khởi tạo trước đó nhưng không sử dụng trực tiếp như ở trên được mà phải `append`

```go
slice = append(slice, 30)
```

![[00 Meta/01 Attachments/Pasted image 20230627170536.png]]

```go
slice = append(slice, 40)
```

![[00 Meta/01 Attachments/Pasted image 20230627170558.png]]

- Khi hết thêm hết `capacity`, từ đây, mỗi khi `append` Go sẽ tạo một `array` mới với `capacity + 1` và `length + 1`, copy các giá trị cũ và `append` thêm giá trị mới.

```go
slice = append(slice, 50)
```

![[00 Meta/01 Attachments/Pasted image 20230627170714.png]]

> [!note] Lưu ý
> 
> Cần để ý capacity của 1 slice, tránh việc slice không đủ capacity, mỗi lần thêm một phần tử mới sẽ ảnh hưởng đến performance của hệ thống. 