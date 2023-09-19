---
title: "🌱 What is Vue?"
tags: [vuejs]
date: 2022-12-24
---

## 🌿 What is Vue?

![[00 Meta/01 Attachments/Pasted image 20221224114448.png]]
- Vuejs là một open source Javascript framework hướng tới việc xây dựng giao diện người dùng(UI), được tạo ra bởi [Evan You](https://twitter.com/youyuxi?lang=en). Như trên [Landing page](https://vuejs.org/) có giới thiệu, Vuejs là một phiên bản cấp tiến của Javascript framework với những đặc điểm nổi bật như dễ tiếp cận, linh hoạt và hiệu quả. 

## 🌿 Why use it?

### 🌱 Progressive - Cấp tiến

- Vue được công nhận là **progressive** vì nó thường có thể scale down cũng như up. Với đa số những trường hợp sử dụng phổ thông, chúng ta có thể tích hợp Vue như jQuery - thêm một script tag như sau: 

```html
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

- Khi nhu cầu sử dụng của chúng ta phát triển, Vue cũng sẽ cung cấp thêm những công cụ có trong hệ sinh thái giúp nâng cao hiệu quả sử dụng. 
  
### 🌱 Approachable - Dễ tiếp cận

- Vue rất dễ tiếp cận miễn là chúng ta có hiểu biết HTML, CSS, và JS tiêu chuẩn. Vậy là bạn có thể bắt đầu làm việc với Vue được rồi. 

### 🌱 Versatile - Linh hoạt

![[00 Meta/01 Attachments/Pasted image 20221224114549.png|80%]]

- Vue linh hoạt vì xung quanh thư viện có đầy đủ các tools support, muốn dùng gì thì mình tích hợp thêm, chứ không cần phải cài hết một lượt. Các tools phổ biến:
	- [vue-cli](https://cli.vuejs.org/) (i.e. Vue Command Line Interface) - như cli của những framwork khác, cho phép giao tiếp nhanh cong với Vue app.
	- [vue-router](https://router.vuejs.org/) - chỉ định routes giao tiếp dễ dàng giữa client-side và server-side.
	- [vuex](https://vuex.vuejs.org/guide/) - hỗ trợ quản lý dữ liệu.
	- [vue-test-utils](https://vue-test-utils.vuejs.org/) - cung cấp đa dạng các helpers cũn như functions hỗ trợ chúng ta trong quá trình viết UT.

- Các tools trên đều được created and maintained bởi chính đội Vue core nên việc tích hợp sẽ vẫn là trơn chu, mượt mà.
  
### 🌱 Performant - Hiệu quả

![[00 Meta/01 Attachments/Pasted image 20221224120158.png]]

- Cuối cùng, Vue hiệu quả vì nó tận dụng virtual DOM để có được thời gian re-render lại cực nhanh. Thư viện lõi của Vue cũng được phát triển với tiêu chí là tối ưu hiệu suất.

