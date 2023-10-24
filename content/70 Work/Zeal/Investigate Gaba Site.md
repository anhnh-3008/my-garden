---
title: Investigate Gaba Site
date: 2023-10-04
draft: true
---
Link Jira: https://zeals-japan.atlassian.net/browse/CS-89 Gaba

URL: https://secure2.gaba.co.jp/pc_fm_form.html?s=4&lpt=1&crt=2&cs=30&_gl=1*17e7pkd*_ga*MTc1MDgzNDI1My4xNjg3NDIyMzAw*_ga_P4VME74WG3*MTY4NzQyMjMwMC4xLjAuMTY4NzQyMjMwMC42MC4wLjA.

Có 2 sites:
- Site cho hs tiểu học đăng ký: https://secure2.gaba.co.jp/pc_kids_fm_form.html?s=2&lpt=4&crt=8&cs=30
- Site cho các hs khác đăng ký: https://secure2.gaba.co.jp/pc_fm_form.html?s=4&lpt=1&crt=2&cs=30&_gl=1*17e7pkd*_ga*MTc1MDgzNDI1My4xNjg3NDIyMzAw*_ga_P4VME74WG3*MTY4NzQyMjMwMC4xLjAuMTY4NzQyMjMwMC42MC4wLjA.

### API
- [x] API getArea
- [x] API getClass theo area
	- Lấy toàn bộ class trên select.
	- Lấy được mảng area chứa codes của các lớp học(trong file js)
	- Lọc theo area đã chọn
- [ ] API getCalendar chia làm 2 APIs:
	- [x] getDates ngày available luôn tính từ currentDate + 90 ngày.
	- [ ] getTimeSlots
		1. GetPage lấy các timeSlots default.
		2. Từ ngày đã chọn -> tìm data type
			1. Nếu không có -> trả về không có time -> người dùng chọn lại ngày
			2. Nếu có -> Điều chỉnh lại data type theo logic dưới đây.
				- Điều chỉnh lại data type, nếu có là kiểu HOLIDAY và selectedDate in businessHour, ưu tiên cái nào có start và end là 00:00:00
		3. Tìm lsBusinessHours như logic dưới.
			- Lấy businessHours, nếu có key -> lấy luôn. Nếu không có key, kiểm tra có phải là SUNDAY hoặc SATURDAY ko, nếu phải + có key HOLIDAY => return không thì return key NORMAL nếu có key. Nêú tất cả không có => return nil. => lấy được start với end.
		4. Nếu không tìm được lsBusinessHours thì dùng systemBusinessHours.
		5. Loại bỏ những timeSlot nào không nằm trong khoảng start, end tìm được ở bước 4.
- [x] API getAges
- [x] API getJobs
- [x] API getJobCategories

#### ❓Questions
- [ ] Có cần làm 2 sites không?
- [ ] Confirm làm theo datepicker?
- [ ] Có làm phần Multiple checkbox hay không?

![[00 Meta/01 Attachments/Pasted image 20231009100743.png]]