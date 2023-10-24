---
title: Implement Magical Click for Kireilign
date: 2023-10-02
draft: true
---
Repo: https://github.com/zeals-co-ltd/formless

##### Progress
- [x] Install + run app
- [x] Research
- [x] Implementing
- [x] UnitTest

##### Code done
- [x] Fix lint: `yarn prettier:write`
- [x] ...


##### Question?
- [x] Do implement magical click for both kid and adult site? NO


- Thay viết Magical click thành code luôn trên form automation, sử dụng javascript thuần.

Code on browser:
```js
// Create 2 input elements to save value of selected time
var tmp_date_input_name = 'TMP_DATE_INPUT';
var tmp_date_input = document.createElement('input');
tmp_date_input.name = tmp_date_input_name;
document.querySelector('body').append(tmp_date_input);
var tmp_time_input_name = 'TMP_TIME_INPUT';
var tmp_time_input = document.createElement('input');
tmp_time_input.name = tmp_time_input_name;
document.querySelector('body').append(tmp_time_input);

// Script clickToNextCalendar
let requestDate = document.querySelector('input[name="TMP_DATE_INPUT"]').value;
let requestTimeValue = document.querySelector('input[name="TMP_TIME_INPUT"]').value
let requestTime = requestTimeValue.slice(0,2) + ':' + requestTimeValue.slice(2,4);
let yearMonthStr = document.querySelector('.booking-calendar__content > table > thead > tr:nth-child(1) > th:nth-child(2)').textContent.trim().replace(/年|月/g, '/');
let firstDateStr = document.querySelector('.booking-calendar__content > table > thead > tr:nth-child(2) > th:nth-child(1)').textContent;
let firstTime = new Date(yearMonthStr + firstDateStr);
let duration = Math.floor((new Date(requestDate) - firstTime) / (3600000*24));
let nextCalendar = Math.floor(duration/14);

async function delay(ms) {
	return new Promise((resolve) => {
		setTimeout(resolve, ms);
	});
};

async function clickToNextCalendar(nextCalendar) {
	for(let i=0; i<nextCalendar; i++) {
		document.querySelector('.booking-calendar__header.anchor-3 > div.booking-calendar__action > button:nth-child(2)').click();
		await delay(2000);
	}
}

clickToNextCalendar(nextCalendar);

// Script clickTimeSlot
let xPosition = (duration % 14) + 2;
let yPosition = 0;

timeSlotLabels = document.querySelectorAll('.booking-calendar__content > table > tbody > tr > td:nth-child(1)');
for (let i=0; i< timeSlotLabels.length; i++){
	if (requestTime == timeSlotLabels[i].textContent) {
		yPosition = i + 1;
		break;
	}
}

if (yPosition !=1) {
	let xPositionValue = xPosition;
	for (let i = 2; i <= xPositionValue; i++) {
		if (document.querySelector(`.booking-calendar__content > table > tbody > tr:nth-child(1) > td:nth-child(${i})`).className.includes('booking-calendar__item--off')) xPosition--;
	}
}

document.querySelector(`.booking-calendar__content > table > tbody > tr:nth-child(${yPosition}) > td:nth-child(${xPosition})`).click();
```

Status: Done ✅

