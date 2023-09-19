---
title: "🌱 Pipe Data between Programs"
tags: [til, os]
date: 2022-10-30
---

- 🌱 Trong Shell, The Pipe cho phép kết hợp giữa nhiều commands trên cùng một dòng. Được kí hiệu bằng ký tự ASCII 124 ( | ), dấu gạch dọc.

```sh
VD1:
🌱 kết hợp câu lệnh tìm kiếm theo pattern và đếm có bao nhiêu lines trả về từ grep

> grep /bin/bash$ [PATTERN] | wc -l
```

![](https://lh3.googleusercontent.com/P_MDCWdC8VPh8ZMVK3p-MxX8uWYP2w2XFv9mEeMoIudE4x9hJw4S5OaAMjaIRn6Utr8gjNVSSVg89VtDzlL5TI-PUwcDJEM24e-ylJUzcIMpeNFSvTnbrDbctMs8FHrnp_xQ8Mz-jf4pNJzsGQ-79Tf1hTenyIh1fAGdLqz5DS4X9KAtvQVhaVv358Qi)

### Nguồn
- LPIC - 1 - trang 105 