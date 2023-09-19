---
title: "🌱 Generic in Golang"
tags: [golang]
date: 2023-06-29
alias: [generic]
---

- Các function có thể được viết để sử dụng chung cho nhiều Type
```go
func Index[T comparable](s []T, x T) int {
	for i, v := range s {
		if v == x {
			return i
		}
	}
	return -1
}

func main() {
	// Index works on a slice of ints
	si := []int{10, 20, 15, -10}
	fmt.Println(Index(si, 15))

	// Index also works on a slice of strings
	ss := []string{"foo", "bar", "baz"}
	fmt.Println(Index(ss, "hello"))
}

// => 2
// => -1
```
