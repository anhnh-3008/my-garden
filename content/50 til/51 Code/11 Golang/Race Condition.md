---
title: "🌱 Race Condition"
tags: [til, golang]
date: 2023-08-17
---

## 🌿 What?
- Race condition là trường hợp xảy ra khi thiết bị hoặc hệ thống của chúng ta cố gắng thực hiện hai hay nhiều tiến trình xử lý tại một thời điểm trên cùng một resource(một biến, một vùng nhớ, ...) dẫn đến những kết quả không chính xác.
- Race condition thường xảy ra khi hệ thống xử lý các **tác vụ đồng thời** như [[50 til/51 Code/11 Golang/Goroutines|Goroutines]] trong Golang.
![[00 Meta/01 Attachments/Pasted image 20230817102015.png]]
## 🌿 Detecting Race Condition
- Trước tiên, để xử lý Race Condition, chúng ta cần phải xác định hệ thống có đang tồn tại Race Condition hay không. Go đã chu đáo chuẩn bị sẵn **data race detector**, để sử dụng chúng ta chỉ cần thêm flag `-race` như sau:
```sh
$ go test -race mypkg    // to test the package
$ go run -race mysrc.go  // to run the source file
$ go build -race mycmd   // to build the command
$ go install -race mypkg // to install the package
```

## 🌿 Solving with Golang
- Có hai cách thường được sử dụng:
-  🌱 Sử dụng channel: chuẩn Go, Go cung cấp channel để giao tiếp dữ liệu giữa các tiến trình nên việc đọc ghi dữ liệu vào channel sẽ không xảy ra race condition.
```go
import sync

var wg sync.WaitGroup()
for tagDate := currentDate; tagDate.Before(eDate); tagDate = tagDate.AddDate(0, 0, 7) {
	c := make(chan string) 
	wg.Add(1)
	go func () {
		defer func () {
			close(c)
			wg.Done()
		}
		// Get API and return data
		c <- data
	}()
}
wg.Wait()
```
- Nhưng thực tế trong quá trình phát triển, đôi khi chúng ta muôn lưu giá trị vào một biến có type phức tạp chứ không phải channel. Ví dụ như:
```go
import sync

type Calendar struct {
	Holidays []time.Time
	TimeSlots []*TimeSlot
}

type TimeSlot struct {
	Start time.Time
	End time.Time
}
var wg sync.WaitGroup()
var calendar Calendar
for tagDate := currentDate; tagDate.Before(eDate); tagDate = tagDate.AddDate(0, 0, 7) {
	wg.Add(1)
	go func () {
		defer wg.Done()
		// Get API and return data
		calendar = data.Calendar
	}()
}
wg.Wait()
```
- 🌱 Nếu viết như trên chắc chắn sẽ dính race condition và cách fix đó là sử dụng `sync.Mutex`. Chúng ta có thể `Lock` và `Unlock` quá trình ghi dữ liệu vào một ô nhớ, tránh việc nhiều tiến trình cùng xử lý tại một thời điểm.
```go
import sync

type Calendar struct {
	Holidays []time.Time
	TimeSlots []*TimeSlot
}

type TimeSlot struct {
	Start time.Time
	End time.Time
}
var wg sync.WaitGroup()
var mu sync.Mutex()
var calendar Calendar
for tagDate := currentDate; tagDate.Before(eDate); tagDate = tagDate.AddDate(0, 0, 7) {
	wg.Add(1)
	go func () {
		defer wg.Done()
		// Get API and return data
		mu.Lock()
		calendar = data.Calendar
		mu.Unlock()
	}()
}
wg.Wait()
```

## 🌿 Refer
- [Race Detector](https://go.dev/doc/articles/race_detector)
- [What are race conditions in Golang?](https://www.educative.io/answers/what-are-race-conditions-in-golang)