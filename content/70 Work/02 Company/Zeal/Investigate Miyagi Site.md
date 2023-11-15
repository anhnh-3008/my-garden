---
title: Investigate Miyagi Site
date: 2023-09-28
draft: true
---
Link Jira: https://zeals-japan.atlassian.net/browse/CS-63 - Kireilign

Làm 2 RPA builders:
- Form1: https://lp.kireilign.com/yoyaku/?ads=zeals 
- Form2: https://lp.kireilign.com/yoyaku/tokyo?ads=zeals&brand=kids


### Get Prefecture  >  Station API ✅
- Dùng API của client: 
	- URL: https://lp.kireilign.com/api/prefectures/clinic?version=2&is_sort_by_id=true
- Xử lý nearest_station để đếm số phòng khám gần 1 ga, hiển thị số nếu > 2.
### Get Clinic ✅
- Dùng API của client: 
	- URL: https://lp.kireilign.com/api/prefectures/clinic?version=2&is_sort_by_id=true
### Get Calendar
- Dùng API của client: 
	- URL: https://lp.kireilign.com/api/efo/v2/available-schedule?clinic_id=5237&date=2023-09-29&number_of_days=13&checkSkip=false


#### 🚫 Vấn đề
- [x] Tìm giải pháp đếm Phòng khám gần Ga tàu
- [x] Kiểm tra có cần phải làm Magical Click không?
- [ ] Tìm giải pháp fill giá trị vào form(input không có attribute định danh như id, name)
- [ ] Tìm logic xác định time limit
- [ ] Tìm hiểu implement magical click

#### 🔍 Client Investigate Rubric
- Scrapper Implementation: 3 - has 2 dependencies: get Stations, get Clinic Room
- Automation Form: 3
- Magical Click: 