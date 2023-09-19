---
title: "🌱 DATE_SUB - ngược về quá khứ"
tags: [til, mysql]
date: 2022-11-09
---

- 🌱 Trong SQL, hàm `DATE_SUB()` trả về ngày sau khi đã lùi một khoảng thời gian chỉ định.

```sql
DATE_SUB(date, INTERVAL value unit)

# date: Ngày làm mốc.
# value: thời gian bị trừ(có thể chỉ định giá trị âm || dương)
# unit: đơn vị thời gian(ngày, giờ, phút, ...)
```