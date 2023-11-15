---
title: 🌱 Sử dụng Cypress để test Crawl dữ liệu
tags:
  - til
date: 2023-10-26
aliases:
  - cypress
draft: false
---
Dự án mình đang làm cần build các APIs để crawl datas từ client page. Cơ mà sau khi implement xong code và đưa cho QA test thì có những site phát sinh nhiều bugs và mình muốn cải thiện điều này. Thế là mình có hỏi được bên QA(anh ấy tên là Xuân, đẹp zai như diễn viên HongKong luôn 😎) mọi người đang sử dụng tool [Cypress](https://www.cypress.io) để chạy automation test, tiện ngồi setup mình viết lại doc sau này xem lại cho tiện.
# 🌿 What?
![[00 Meta/01 Attachments/Pasted image 20231026104258.png]]

Cypress là một *front end testing tool* thế hệ mới được build để phục vụ kiểm thử tự động trên giao diện của website.

> Cypress can test anything that runs in a browser.
> *This enables you to **write faster**, **easier** and **more reliable** tests.*
> — <cite>Cypress's Document</cite>


# 🌿 Features
- **Time Travel**: Cypress snapshots lại từng bước, tiện cho việc theo dõi giao diện ở từng bước.
- **Debuggability**:  Không cần phải đoán già đoán non sao testcase nó fail nữa, có thể debug trực tiếp như trên Developer Tools.
- **Automatic Waiting**: Tự động chờ commands and assertions trước khi tiếp tục. Không cần phải dò đặt sleep hay bị dính callback hell nữa.
- **Network Traffic Control**: Có thể control + stub được traffic network. Test tải, test cạnh tranh, ....
- **Cross Browser Testing**: Chạy được trên Firefox, Chrome, Edge và Electron.

[*xem thêm*](https://docs.cypress.io/guides/overview/why-cypress#Features)


# 🚧 Implement
## 📝 Common

> [!note] describe, it là gì?
> 
> Hiểu đơn giản describe, context, it hay specify là đầu mục giải thích behaviors của các testcases, làm cho bộ test có tổ chức và dễ đọc hơn.
> - context() có thể coi là alias của describe()

> [!note] Hook là gì?
> 
> Tiện nói luôn về hook, có thể chúng ta sẽ gặp trong quá trình implement.
> Hook giúp thực hiện một hành động tại thời điểm trước hoặc sau của một hoặc nhiều test cases.
> - before()/after()
> - beforeEach()/afterEach()

> [!note] only() và skip()
> - .only() sẽ chỉ chạy những testcase được chỉ định
> - .skip() sẽ bỏ qua những testcase được chỉ định
> 
> Note: Hook nếu được define sẽ luôn được excute

## 1️⃣ Visit a page
Dùng method `visit()` để truy cập tới URL cần test.
```js
describe('Test The Client Site', () => {  
	it('Visits the Client Sink', () => {  
		cy.visit('https://example.client.com')  
	})  
})
```


## 2️⃣ Trigger or Assertion
Giờ thì muốn test thao tác gì thì mình triển thoai 💪
- Ví dụ mình muốn lấy tất cả các options area trên client page và compare với một mảng giá trị areas có sẵn.

```js
describe('Test The Client Site', () => {
	const url = "https://client.com"
	var areaList = ["東京都", "関東", "中部", "関西", "中国・四国", "九州", "その他"];
	
	before (function () {
		cy.visit(url);
		cy.get('select[name="area"]').find('option').each((res) => {
			var index = areaList.indexOf(res.text());
			if (index > -1) areaList.splice(index, 1);
		})
	})
	
	it('Compare list areas on the client page', () => {
		cy.expect(areaList).to.equal([]);
	})
})
```

![[00 Meta/01 Attachments/Pasted image 20231026153931.png]]
# 🌿 Refer 
- https://docs.cypress.io/guides/end-to-end-testing/writing-your-first-end-to-end-test
