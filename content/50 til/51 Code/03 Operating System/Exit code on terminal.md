---
title: "🌱 Exit code on terminal"
tags: [til, os]
date: 2022-12-14
---

## 🌿 Run multi commands in on line on terminal

```bash
$> command1; command2; command3
```  

-   Sẽ luôn excute hết các câu lệnh, kể cả khi các câu lệnh ở trước nó bị lỗi.

-    Nhưng nếu cần sự ràng buộc **phải đúng** ở các câu lệnh trước thì mới được chạy tiếp, vd như `apt-get update`  và `apt-get install package` , dùng dấu `&&`

```bash
$> apt-get update && apt-get install package
```  

## 🌿 Exit code in shell

-   Như bên trên có nói đến việc check đúng - các câu lệnh chạy thành công được xác định bởi **Exit Code.**
	-   **Exit code** trả về 0 -> success
	-   **Exit code** trả về khác 0, có giá trị từ 1-255 -> nghĩa là câu lệnh chạy có lỗi
-   Check Exit Code của câu lệnh gần nhất:

```bash
$> who
=> hoanganh8999 :1           2022-12-14 19:24 (:1)

$> echo $?
=> 0

$> wo
=> wo: command not found

$> echo $?
=> 127
```

## 🌿 Refer 

- [https://mazer.dev/en/linux/tips/how-to-determine-error-and-exit-main-shell-script/](https://mazer.dev/en/linux/tips/how-to-determine-error-and-exit-main-shell-script/)