---
title: "🌱 Goroutines"
tags: [golang]
date: 2023-06-29
alias: [goroutines]
---
![[00 Meta/01 Attachments/Pasted image 20230629162325.png]]

- Khía cạnh mạnh mẽ nhất của Go so với các ngôn ngữ lập trình khác chính là khả năng xử lý các methods **độc lập** và **đồng thời**.

- Trước đó, cần làm rõ, một **process** và một **thread** là gì.
- 🌱 Process: hiểu đơn giản là một chương trình đang chạy trong máy tính.
- 🌱 Thread: Là các luồng chạy bên trong một tiến trình.


## 🌿 What?
- Là một **lightweight thread** được quản lý bởi **Go runtime**.
- Trong bất kỳ một chương trình Golang nào, đều tồn tại ít nhất một Goroutine, gọi là **main Goroutine**. Nếu main goroutine kết thúc, toàn bộ các goroutones khác trong tiến trình cũng sẽ kết thúc ngay.
- Goroutine sử dụng tối ưu hơn Thread truyền thống rất nhiều.

|Thread|Goroutine|
|-------|----------|
|Được quản lý bởi hệ điều hành và phụ thuộc vào số nhân CPU|Được quản lý bởi **go runtime** và không phụ thuộc vào nhân CPU|
|Size vùng nhớ **stack** cố định|Size vùng nhớ **stack** linh động cấp phát theo khả năng sử dụng|
|Giao tiếp khó, có độ trễ lớn trong tương tác|Sử dụng channel để tương tác với nhau, độ trễ thấp|
|Có định danh|Không có định danh|
|Khởi tạo và giải phóng tốn nhiều thời gian| Khởi tạo và giải phóng bởi **go runtime** nên rất nhanh|

> [!question] Câu hỏi?
> 
> go runtime là cái gì mà nó có thể khởi tạo và giải phóng các goroutines nhanh như thế?


## 🌿 Channel
- Là chỗ lưu trữ vùng nhớ **stack**
```go
ch := make(chan int)

ch <- v // send v to channel ch
v := <-ch // receive value from ch and assign value to v
```

- Để tránh việc ghi bừa phứa dữ liệu vào vùng nhớ **stack**, Go chỉ cho phép gửi value vào channel khi có chỗ lấy ra value đó.
```go
ch := make(chan int)
ch <- v
// nếu không có chỗ nhận v, hệ thống sẽ báo fatal error
// fatal error: all goroutines are asleep - deadlock!
```

- Để giải quyết vấn đề này, có thể sử dụng **channel buffering**, nó cho phép chúng ta giới hạn giá trị có thể đưa vào channel mà không nhất thiết phải sử dụng.

```go
ch := make(chan int, 3)
ch <- 1
ch <- 2
ch <- 3
```

- Khi hết buffer, sử dụng `close()` để channel không nhận thêm dữ liệu nữa.
```go
func fibonacci(n int, c chan int) {
	x, y := 0, 1
	for i := 0; i < n; i++ {
		c <- x
		x, y = y, x+y
	}
	close(c)
}

func main() {
	c := make(chan int, 10)
	go fibonacci(cap(c), c)
	for i := range c {
		fmt.Println(i)
	}
	v, ok := <-c
	fmt.Println(v, ok)
}
```

- `select` statement sẽ thực thi những communication đã sẵn sàng(có đưa vào channel và lấy ra)

```go
func fibonacci(c, quit chan int) {
	x, y := 0, 1
	for {
		select {
		case c <- x:
			x, y = y, x+y
		case <-quit:
			fmt.Println("quit")
			return
		}
	}
}

func main() {
	c := make(chan int)
	quit := make(chan int)
	go func() {
		for i := 0; i < 10; i++ {
			fmt.Println(<-c)
		}
		quit <- 0
	}()
	fibonacci(c, quit)
}
// print 0 -> 34
// quit
```

- `default case` sẽ được thực hiện khi không có `case` nào phù hợp.
``` go
select {
	case <-ch:
		// code
	case <-ch:
		// code
	default:
		//code
}
```

- `sync.Mutex` cung cấp 2 methods giúp `Lock` và `Unlock` một goroutine. Được cung cấp từ package `sync`.
```go
import (
	"sync"
)

// SafeCounter is safe to use concurrently.
type SafeCounter struct {
	mu sync.Mutex
	v  map[string]int
}

// Inc increments the counter for the given key.
func (c *SafeCounter) Inc(key string) {
	c.mu.Lock()
	// Lock so only one goroutine at a time can access the map c.v.
	c.v[key]++
	c.mu.Unlock()
}
```
