# Response of API
Về cơ bản, Azure sẽ có mô hình AI đánh giá content mình gửi lên theo 4 categoris: Hate, SelfHarm, Sexual và Violence. Mỗi mục sẽ được AI đánh giá và cho điểm(có thể tùy chọn theo tháng điểm 4 hoặc 8). ĐIểm càng cao thì mức độ vi phạm càng nghiêm trọng.

- Document mô tả cách tính điểm của model. Mình sẽ thống nhất với khách từng mục một có giới hạn điểm bao nhiêu là bị block, không cho tạo bài viết. Ví dụ Hate > 3 => vi phạm chuẩn mực => không tạo bài viết.

https://learn.microsoft.com/en-us/azure/ai-services/content-safety/concepts/harm-categories?tabs=definitions

- Response của Moderate text:

```
# blocklistsMatch sẽ hiển thị các từ mình chỉ định là vi phạm chuẩn mực(custom). Nếu không chỉ định, Azure sẽ chỉ trả về điểm của các categories.
{
  "blocklistsMatch": [ 
    {
      "blocklistName": "ProfanityBlocklist",
      "blocklistItemId": "12345",
      "blocklistItemText": "inappropriate_word"
    }
  ],

  "categoriesAnalysis": [
    {
      "category": "Hate",
      "severity": 2
    },
    {
      "category": "SelfHarm",
      "severity": 0
    },
    {
      "category": "Sexual",
      "severity": 0
    },
    {
      "category": "Violence",
      "severity": 0
    }
  ]
}
```

- Response của Image text:

```
{
  "categoriesAnalysis": [
    {
      "category": "Hate",
      "severity": 2
    },
    {
      "category": "SelfHarm",
      "severity": 0
    },
    {
      "category": "Sexual",
      "severity": 0
    },
    {
      "category": "Violence",
      "severity": 0
    }
  ]
}
```

# Integrate to code
- Tạo một Class thực hiện việc khởi tạo object có nhiệm vụ call API của Azure.
- Class gồm thuộc tính là blocklistsMatch và phương thức `moderateText`, `moderateImage`.
- Ở các API create/update post, gọi các phương thức `moderateText`, `moderateImage` để validate dữ liệu.