---
title: 🌱 Split array by an value
tags:
  - til
  - ruby
date: 2023-09-15
aliases: 
draft: false
---
Trong ruby, khi muốn split một array ra 2 arrays theo value, có thể sử dụng method `slice_after`(method `slice_before` cũng tương tự, chỉ khác vị trí split)

```ruby
array = [
  {activity: "1", ticket: "123"},
  {activity: "2", ticket: "123"},
  {activity: "3", ticket: ""},
  {activity: "4", ticket: "234"},
]

array.slice_after { |i| i.activity == "3" }
# Returns:
[
  [
    {activity: "1", ticket: "123"},
    {activity: "2", ticket: "123"},
    {activity: "3", ticket: ""}
  ],
  [
    {activity: "4", ticket: "234"}
  ]
]

array.slice_before { |i| i.activity == "3" }
# Returns:
[
  [
    {activity: "1", ticket: "123"},
    {activity: "2", ticket: "123"}
  ],
  [
    {activity: "3", ticket: ""},
    {activity: "4", ticket: "234"}
  ]
]
```


https://til.hashrocket.com/posts/rm9tvmzf9p-using-sliceafter-to-split-arrays-by-a-value-