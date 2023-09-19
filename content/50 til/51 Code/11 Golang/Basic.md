---
title: "🌱 Golang basic"
tags: [golang]
date: 2023-06-27
alias: []
draft: true
---

## 🌿 Packages, Variables, Functions

- Mỗi chương trình của Go đều được tạo thành từ các packages. 
- Name export từ một package phải viết hoa chữ cái đầu
``` go
math.pi => error
math.Pi
```

- Function cần chỉ định kiểu dữ liệu trả về(like C++)
``` go
func add(x int, y int) int {
	return x + y
}

// or shorthand

func add(x, y int) int {
	return x + y
}
```

- Function return nhiều giá trị
```go
func swap(x, y string) (string, string) {
	return x, y
}
```

- Có thể define return các giá trị trong một func. Nhưng cách này có thể sẽ gây khó hiểu với những func dài.
``` go
fucn split(sum int) (x, y int) {
	x = sum + 1
	y = sum - 1
	return
}
```

- Khởi tạo một biến
``` go
var i, j int = 1, 2

// or 

var i, j = 1, 2

// or 

i, j := 1, 2
```

## 🌿 Flow control

- Trong Go chỉ có một cấu trúc lặp là `for`, có 3 thành phần giống C++
	- biến khởi tạo
	- điều kiện dừng
	- trigger biến khởi tạo(tăng/giảm tiến tới điều kiện dừng)

> **Note:** Unlike other languages like C, Java, or JavaScript there are no parentheses surrounding the three components of the `for` statement and the braces `{ }` are always required

``` go 
sum := 0
for i := 0; i < 10; i++ {
	sum += i
}
```

- Biến khởi tạo có thể là optional
``` go
sum := 0
for ; sum < 1000; {
	sum += 100
}
```

- Hoặc có thể viết như `while`
``` go
sum := 0
for sum < 1000 {
	sum += 100
}
```

- Nếu không có điều kiện dừng sẽ lặp vô hạn.

- `if` giống `for` là không cần `( )` nhưng phải có `{ }`
``` go
sum := 1
if sum > 0 {
	return "Positive"
}
```

- Có thể sử dụng một short statement trước khi kiểm tra điều kiện trong `if`
``` go
if sum := 1; sum > 0 {
	return "Positive"
}
```

- Biến được khởi tạo trên short statement có thể sử dụng trong `else`, nhưng không sử dụng được ở ngoài `if`, `else`.

- `defer` các đối số được đánh giá ngay khi được gọi nhưng function sẽ được excute sau khi các functions cùng cấp trả về kết quả. `Stacking - Last In First Out`
``` go
func main() {
	defer fmt.Println("world")

	fmt.Println("hello")
}

=> hello
=> world
```

## 🌿 Types: Pointers

### 🌱 Pointers
- Con trỏ sẽ trỏ đến địa chỉ bộ nhớ của một giá trị.
```go
i := 1

p := &i // trỏ tới i
fmt.Println(*p) // đọc giá trị của i thông qua con trỏ p
*p = 21 // set giá trị mới cho i thông qua con trỏ p
```

- `struct` là một collection các field, kiểu như một object
``` go
type Vertex struct {
	X int
	Y int
}

func main () {
	v := Vertex{1, 2}
	v := Vertex{X: 1} // Y =0
	v := Vertex{} // X, Y = 0, 0
	v.X = 4
	fmt.Println(v.X)
}

=> 4
```

- Bình thường sử dụng con trỏ phải có `*`, nhưng nếu dùng với `struct` sẽ bị cồng kềnh(`(*p).X`)
```go
v := Vertex{1,2}
p := &v;
p.X = 4
fmt.Println(p.X)
```

### 🌱 Array
- `array`, độ dài của mảng là một phần của kiểu dữ liệu, vậy nên không thể thay đổi độ dài của `array`
```go
numbers = [4]int{1,2,3,4}
strings = [2]string{"hello", "world"}
```

### 🌱 [[50 til/51 Code/11 Golang/Slice in Golang|Slice]]
- `[[50 til/51 Code/51.11 Golang/Slice in Golang|slice]]` ảnh hưởng trực tiếp tới `array`
```go
names := [4]string{
		"John",
		"Paul",
		"George",
		"Ringo",
	}
	fmt.Println(names)

	a := names[0:2]
	b := names[1:3]
	fmt.Println(a, b)

	b[0] = "XXX"
	fmt.Println(a, b)
	fmt.Println(names)

=> [John Paul George Ringo]
=> [John Paul] [Paul George]
=> [John XXX] [XXX George]
=> [John XXX George Ringo]
```

- `slide` không cần chỉ định độ dài.
- Đọc thêm về [[50 til/51 Code/11 Golang/Slice in Golang|cơ chế hoạt động của slice ]]

- `range` để lặp `[[50 til/51 Code/51.11 Golang/Slice in Golang|slice]]`
```go
pow := []int{1,2,3,4}

for i, v := range {
	fmt.Printf("2**%d = %d\n", i, v)
}

// 2**0 = 1
// 2**1 = 2
// 2**2 = 4
// 2**3 = 8
```

- Có thể skip index hoặc value
```go
for _, value := range pow {
		fmt.Printf("%d\n", value)
}
```

### 🌱 Maps
- Lưu dữ liệu dưới dạng key/value. Truy xuất dữ liệu nhanh hơn `array` và  `[[50 til/51 Code/51.11 Golang/Slice in Golang|slice]]` thông qua key.
```go
map := map[string]int{"1": 1, "2": 2}
// string là kiểu dữ liệu của key
// int là kiểu dữ liệu của value
// key không thể là slices, arrays hoặc functions
```

### 🌱 Functions
- Func có thể được gán cho một biến, và nó cũng có thể là một tham số truyền vào.
```go
func compute(fn func(float64, float64) float64) float64 {
	return fn(3, 4)
}

func main() {
	hypot := func(x, y float64) float64 {
		return math.Sqrt(x*x + y*y)
	}
	fmt.Println(hypot(5, 12))

	fmt.Println(compute(hypot))
	fmt.Println(compute(math.Pow))
}
```