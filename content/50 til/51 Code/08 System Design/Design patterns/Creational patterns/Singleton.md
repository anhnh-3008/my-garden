---
title: 🌱 Singleton
tags:
  - til
  - design-patterns
date: 2023-10-25
aliases:
  - singleton
draft: false
---
# 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20231025133825.png]]

Singleton là pattern thiết kế đảm bảo việc **một class chỉ có duy nhất một instance được khởi tạo và sử dụng cho toàn bộ hệ thống.**

Singleton giải quyết 2 vấn đề:
1. **Một class chỉ có một instance được khởi tạo tại một thời điểm.** 
	- Lý do phổ biến nhất đó là dễ dàng kiểm soát truy cập tới những tài nguyên chung - ví dụ database hoặc 1 file.
2. **Cung cấp truy cập cho toàn bộ hệ thống.**
	- Thường khi muốn lưu những thông tin thiết yếu của một vài objects, chúng ta có thể sử dụng một global variable. Cách này nhanh nhưng không an toàn, do global variable có thể bị ghi đè ở bất kỳ đâu trong hệ thống.
	- Thay vì đó Singleton sẽ cung cấp khả năng truy cập nhưng không ghi đè dữ liệu lên instance được.

> [!example] Example
> 
>  Sử dụng Singleton khởi tạo connection cho database. Chỉ một class ConnectionDB chịu trách nhiệm tạo duy nhất một connection instance tới DB và toàn bộ hệ thống chỉ được truy cập vào DB thông qua connection instance này.

# 🚧 Structure

![[00 Meta/01 Attachments/Pasted image 20231025135740.png]]

Class gồm 2 thành phần:
1. Private static attribute lưu giá trị của instance.
2. Public method khởi tạo(lazy init) instance.

# 🛠️ Implement Singleton in Golang
 Implement Singleton sử dụng [[50 til/51 Code/11 Golang/Goroutines|Goroutines]].
```go
// single_class.go

package main

import (
    "fmt"
    "sync"
)

var lock = &sync.Mutex{}

type single struct {
}

var singleInstance *single

func getInstance() *single {
    if singleInstance == nil {
        lock.Lock()
        defer lock.Unlock()
        if singleInstance == nil {
            fmt.Println("Creating single instance now.")
            singleInstance = &single{}
        } else {
            fmt.Println("Single instance already created.")
        }
    } else {
        fmt.Println("Single instance already created.")
    }

    return singleInstance
}
```

```go
// main.go
package main

import (
    "fmt"
)

func main() {

    for i := 0; i < 30; i++ {
        go getInstance()
    }

    // Scanln is similar to Scan, but stops scanning at a newline and
    // after the final item there must be a newline or EOF.
    fmt.Scanln()
}
```

# 📜 References
- https://refactoring.guru/design-patterns/singleton