---
title: "📑 Same-origin policy"
tags: [til, sys design]
date: 2022-10-01
---


## 🌿 What?
-  Là một cơ chế bảo mật hạn chế việc `documents` hoặc `script load` thuộc một `origin` có thể tương tác với những `resources` thuộc một `origin` khác.
-  Được cài đặt vào toàn bộ  các trình duyệt hiện nay.
-  Chính sách này giúp trang web của chúng ta không bị truy cập bừa bãi từ những tác nhân lạ.
	- Ví dụ nếu bạn vào một trang web bất kỳ được cài sẵn một mã độc truy cập đến trang web VCB, nếu bạn đã đăng nhập vào VCB, vẫn còn hiệu lực đăng nhập và không có chính sách này, hacker sẽ chiếm được quyền sử dụng tài khoản ngân hàng của bạn.
	- Còn bình thường mn sẽ nhận được message này ở console browser

```js
Access to XMLHttpRequest at 'https://vietcombank.com/profile' from origin 'xxx' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

- 🌱 Nhưng thực hiện truy vấn giữa nhiều trang web với nhau là việc rất thường xuyên đối với một lập trình viên, đặc biệt là vụ call API. Và thế là Cross-origin Resource Sharing - CORS ra đời =))