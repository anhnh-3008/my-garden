---
title: 🌱 Method and Interface in Golang
tags:
  - golang
date: 2023-06-28
aliases:
  - method
  - interface
draft: false
---

## 🌿 Method
- Trong Golang không có Class. Để build các instance method, chúng ta có thể build trực tiếp với type
```go
type Vertex struct {
	X, Y int
}

func (v Vertex) Abs() int {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func main {
	v := Vertex{1,2}
	fmt.Println(v.Abs())
}
```

- Có thể define một method với type không phải struct.
```go
type MyFloat float64

func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}
```

- Để thay đổi giá trị của một instance, cần sử dụng **pointer receiver** làm tham số
```go
type Vertex struct {
	X, Y float64
}

func (v Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func (v *Vertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

func main() {
	v := Vertex{3, 4}
	v.Scale(10) // => v = 50
	// if unuse poiter reciever(v Vertex) => v doesn't modify , v = 5
	fmt.Println(v.Abs())
}
// => 50
```

 - ⚠️ Go sẽ bắt chặt kiểu của con trỏ khi nó được truyền vào như một tham số. Còn khi sử dụng method, Go sẽ tự phiên dịch thành con trỏ(giống như khi gọi attributes của 1 con trỏ Struct)
```go
func (v *Vertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

func ScaleFunc(v *Vertex, f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

ScaleFunc(v, 5)  // Compile error!
ScaleFunc(&v, 5) // OK

v.Scale(5)  // OK
p := &v
p.Scale(10) // OK
```
- Vậy lúc nào nên sử dụng pointer receiver?
	- Có 2 use cases cần sử dụng pointer receiver:
		1. method có thể thay đổi được giá trị của instance.
		2. tránh copy giá trị cho các methods gọi đến. Điều này có thể sẽ hiệu quả nếu tham số nhận vào là một large struct và method không cần modify giá trị.

## 🌿 Interface
- Interface là một tập hợp các method signatures.
```go
type Animal interface {
	Say()
}

type Bird struct {
	name string
}

func (b Bird) Say() {
	fmt.Println("I'm a %s", a.name)
}

func main {
	var a A = Bird{"bird"}
	a.Say()
}
```

- type assertions, chỉ định kiểu return của method khi gọi thông qua interface
```go
var i interface{} = "Hello"

s := i.(string)
fmt.Println(s)
// => Hello

f := i.(float64)
// => panic
// để tránh gây lỗi khi sử dụng không đúng kiểu

f, ok := i.(float64)
fmt.Println(f, ok)
// => 0, false
```

- Type Switch, giống Switch thông thường nhưng rẽ nhánh theo type của interface
```go
func do(i interface{}) {
	switch v := i.(type) {
	case int:
		fmt.Printf("Twice %v is %v\n", v, v*2)
	case string:
		fmt.Printf("%q is %v bytes long\n", v, len(v))
	default:
		fmt.Printf("I don't know about type %T!\n", v)
	}
}
```

- Stringer, interface `Stringer()` do package `fmt` cung cấp, xử lý trước output cho `fmt.Println()`
```go
type IPAddr [4]byte

// TODO: Add a "String() string" method to IPAddr.
func (ip IPAddr) String() string {
	return fmt.Sprintf("%v.%v.%v.%v", ip[0], ip[1], ip[2], ip[3])
}


func main() {
	hosts := map[string]IPAddr{
		"loopback":  {127, 0, 0, 1},
		"googleDNS": {8, 8, 8, 8},
	}
	for name, ip := range hosts {
		fmt.Printf("%v: %v\n", name, ip)
	}
}
// googleDNS: 8.8.8.8
// loopback: 127.0.0.1
```

- Tương tự, `fmt` cũng cung cấp interface `Error()` cho việc hiển thị lỗi.
```go
type MyError struct {
	When time.Time
	What string
}

func (e *MyError) Error() string {
	return fmt.Sprintf("at %v, %s",
		e.When, e.What)
}

func run() error {
	return &MyError{
		time.Now(),
		"it didn't work",
	}
}
```
