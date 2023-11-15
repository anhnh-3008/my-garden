---
title: Investigate DentalClinic
date: 2023-10-31
draft: true
---
- Các APIs:
	- [ ] getAreas
	- [ ] getClinics
	- [ ] getCalendar

- [ ] Build RPA Builder giống với Kireilign.

- [ ] Viết test bằng [[50 til/51 Code/07 Utils/Sử dụng Cypress để test Crawl dữ liệu|Cypress]].


Have a nice day, Miyu san!
We have finished investigating the DentalClinic. We want to confirm with you an issue:
- On the client site, step-by-step to select  a clinic is: select prefecture group in an area -> click button select clinic. 
- However, we investigate that each prefecture only has a clinic. So with our webform, we prefer to create 2 APIs: getAreas and getClinics(skip the step select prefectures).

What do you think about that?

And here is our estimated time:
- Implement APIs getAreas, getClinics, getCalendar: 3-4 days
- Build RPA builder: 1-2 days
- QA test: 3-4 days

千葉 - 404 NotFound



Code RUN_SCIPT form automation:
```js
var tmp_address_input_name="TMP_ADDRESS_INPUT",tmp_address_input=document.createElement("input");tmp_address_input.name=tmp_address_input_name,document.querySelector("body").append(tmp_address_input);
var tmp_date_input_name="TMP_DATE_INPUT",tmp_date_input=document.createElement("input");tmp_date_input.name=tmp_date_input_name,document.querySelector("body").append(tmp_date_input);var tmp_time_input_name="TMP_TIME_INPUT",tmp_time_input=document.createElement("input");tmp_time_input.name=tmp_time_input_name,document.querySelector("body").append(tmp_time_input);
```

