---
title: Investigate Rize Clinic
tags:
  - work
date: 2023-12-06
draft: true
---
Ticket: https://zeals-japan.atlassian.net/browse/CS-149
URL: https://www.rizeclinic.com/reserve/
Investigate Template: https://zeals-japan.atlassian.net/wiki/spaces/EUU/pages/818184194/Sun+Investigation+Rize+Clinic+template

Scraper APIs: 
- [ ] getAreas
- [ ] getPrefectures
- [ ] getAreas2
- [ ] getCenterReservations
- [ ] getMenus
- [ ] getCalendar
- [ ] getPlans
- [ ] getNumberOfIrradiations
- [ ] getPayments
- [ ] getYearsOfBirthday


Hi there, Miyu san. I hope you have a productive day!

Our investigation have been finished. I want to clarify with you two below issues:
1. This site has 2 types of forms depending on the selected prefecture.
	- **Type 1(pref: 青森院, 八戸院, 盛岡院, いわき院, 郡山院)**(Ảnh 1)
	- **Type 2(pref: other)**(Ảnh 2)
2. Problem: this site has dynamic multiple check-box, as you know, our system doesn't support it currently. Both of 2 types of forms have dynamic multiple check-box.
	- **In Type 1**, the dynamic multiple check-box at the - ご希望のプラン field.
	- 