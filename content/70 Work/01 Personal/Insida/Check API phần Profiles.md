---
quickshare-date: 2024-02-15 20:57:10
quickshare-url: "https://noteshare.space/note/clsnac0t14441501mwa11aov3t#cc568/nE6VUq+Zg4LWOtE1Jvp54ljLn292dyL8D5az0"
---

### GET /api/v1/users/me ✅
- Tình trạng: chạy ổn, đã trả về thông tin của người dùng. 
### GET /api/v1/users/:id ✅
- Tình trạng: chạy ổn, đã trả về thông tin của người dùng theo id trên URL.

### DELETE /api/v1/users/me ✅
- Tình trạng: chạy ổn, đã xóa được user và session.

### PATCH /api/v1/users/me/update-username ✅
- Tình trạng: chạy ổn
- Case tests:
	- params "username" = "" => báo lỗi trường không được empty ✅
	- params "username" = "test" => đã update username đúng theo params ✅

### PATCH /api/v1/users/me/update-fullname ✅
- Tình trạng: chạy ổn
- Case tests:
	- params "fullname" = "" => báo lỗi trường không được empty ✅
	- params "fullname" = "test" => đã update fullname đúng theo params ✅

### PATCH /api/v1/users/me/update-bio ✅
- Tình trạng: chạy ổn
- Case tests:
	- params "bio" = "" => báo lỗi trường không được empty ✅
	- params "bio" = "test" => đã update bio đúng theo params ✅

### PATCH /api/v1/users/me/update-email ✅
- Tình trạng: chạy ổn
- Case tests:
	- params "email" = "" => báo lỗi trường không được empty ✅
	- params "email" = "test" => báo lỗi invalid email ✅
	- params "email" = "test@gmail.com" => Tạo record OTP và gửi OTP qua mail thành công ✅

### PATCH /api/v1/users/me/update-email/confirm ✅
- Tình trạng: chạy ổn
- Case tests:
	- params {"email" = "", "otp"  = "2073"}=> báo lỗi trường email không được empty ✅
	- params {"email" = "test@gmail.com", "otp"  = ""} => báo lỗi trường otp không được empty ✅
	- params {"email" = "test@gmai", "otp"  = "2073"} => báo lỗi invalid email ✅
	- params {"email" = "test@gmai.com", "otp"  = "xxxx"} => báo lỗi invalid otp ✅
	- params {"email" = "test@gmail.com", "otp"  = "2073(lấy trong DB)"} => update dữ liệu thành công trong DB ✅

### PATCH /api/v1/users/me/update-dob ✅
- Tình trạng: chạy ổn
- Case tests:
	- params "dob" = "" => báo lỗi trường không được empty ✅
	- params "dob" = "2023/01/01" => báo lỗi cần trên 16 tuổi ✅
	- params "dob" = "1999/01/01" => update giá trị thành công ✅

### PATCH /api/v1/users/me/update-phone ✅
- Tình trạng: chạy ổn
- Case tests:
	- params "phone" = "" => báo lỗi trường không được empty ✅
	- params "phone" = "test" => báo lỗi invalid phone ✅
	- params "phone" = "+84949690468" => Tạo record OTP và gửi OTP thành công ✅

### PATCH /api/v1/users/me/update-phone/confirm ✅
- Tình trạng: chạy ổn
- Case tests:
	- params {"phone" = "", "otp"  = "2073"}=> báo lỗi trường email không được empty ✅
	- params {"phone" = "+84949690468", "otp"  = ""} => báo lỗi trường otp không được empty ✅
	- params {"phone" = "+test", "otp"  = "2073"} => báo lỗi invalid phone ✅
	- params {"phone" = "+84949690468", "otp"  = "xxxx"} => báo lỗi invalid otp ✅
	- params {"phone" = "+84949690468", "otp"  = "2073(lấy trong DB)"} => update dữ liệu thành công trong DB ✅

### PATCH /api/v1/users/me/update-password ✅
- Tình trạng: chạy ổn
- Case tests:
	- params "password" = "" => báo lỗi trường không được empty ✅
	- params "password" = "password" => Tạo record OTP thành công ✅

### PATCH /api/v1/users/me/update-password/verify ✅
- Tình trạng: chạy ổn
- Case tests:
	- params "otp" = "" => báo lỗi trường không được empty ✅
	- params "otp" = "xxxx" => Báo lỗi invalid otp ✅

### PATCH /api/v1/users/me/update-password/confirm ✅
- Tình trạng: chạy ổn
- Case tests:
	- params {"password" = "", "otp"  = "2073"} => báo lỗi trường password không được empty ✅
	- params {"password" = "password", "otp"  = ""} => báo lỗi trường otp không được empty ✅
	- params {"password" = "password", "otp"  = "xxxx"} => báo lỗi invalid otp ✅
	- params {"password" = "password", "2073(lấy trong DB)"} => update dữ liệu thành công trong DB ✅
	- params "otp" = "xxxx" => Báo lỗi invalid otp ✅

> [!note] Comment
> Chỗ update password hơi thừa, có thể bỏ bước verify đi và xử lý verify OTP trong API confirm.
#### Luồng update email, password và phone number
- Nhận params là email | password | phone number user muốn update.
- Sau khi verify params
	- Invalid => return lỗi
	- Valid => Tạo một record trong bảng OTP. Nếu là update email or phone thì sẽ gửi OTP về email hoặc phone number tương ứng.
- Confirm update: verify lại OTP code
	- Trùng khớp với record trong DB => update giá trị mới theo params
	- Không trùng khớp với record trong DB => return lỗi.


### Các API còn thiếu so với Figma

#### Profile
- Follow API
- Switch Account API
- Report User API
- Share Profile API
- Block User API

#### Post
- Create API
- Update API
- Update Privacy API
- Delete API
- Pin API
- Flagging content as not interested API
- Handle blur thumbnail for sensitive content

#### Comment
- Report comment API