---
title: "📑 Hệ thống nhận diện liên kết"
tags: [til, sys design]
date: 2022-09-27
---

Hệ thống nhận dạng liên kết( Federated Identity Glossary) là nơi tập trung và liên kết thông tin người dùng. Có 4 yếu tố nền tảng cấu thành nên hệ thống này:
-   **Xác thực (Authentication):** kiểm tra thông tin đăng nhập và tiến hàng định danh người dùng.
-   **Phân quyền (Authorization):** dựa trên thông tin định danh để kiểm tra quyền truy cập của user.
-   **Trao đổi thông tin người dùng (User attributes exchange):** Mỗi hệ thống con sẽ cần và lưu trữ các thông tin khác nhau của người dùng, tuy nhiên sẽ có các thông tin bị lặp lại, ví dụ như tên, họ.... Do đó, cần có một nơi để tổng hợp lại các thông tin này, và trao đổi cho các hệ thống con.
-   **Quản lí người dùng (User management):** admin có thể quản lí người dùng bằng các thao tác thêm, sửa, xóa... ở các hệ thống con.
