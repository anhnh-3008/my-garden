---
title: "🌱 Networking Cost in AWS"
tags: [aws]
date: 2023-04-19
alias: [netwokring cost]
---

## 🌿 Những điều cần lưu ý
![[00 Meta/01 Attachments/Pasted image 20230419214423.png]]
**- Khi thực hiện tạo network trên AWS cần lưu ý:**
	- Sử dụng private network của AWS sẽ rẻ hơn 0.01$ < 0.02$ so với public. Vì private là chúng ta sẽ sử dụng mạng riêng của AWS, còn public thì AWS sẽ phải trả cho chúng ta phần chúng ta sử dụng trên mạng public.
	- Để tối ưu chi phí và trong trường hợp chúng ta muốn các EC2 Instances có thể giao tiếp tính toán với nhau ở tốc độ cao, hãy đặt chúng ở cùng AZ.

![[00 Meta/01 Attachments/Pasted image 20230419215114.png]]
- Egress Traffic: outbound traffics(từ AWS ra ngoài - phải trả tiền)
- Ingress Traffic: inbound traffics(từ ngoài vào AWS - miễn phí)
- Như trên hình, nếu chúng ta lựa chọn đặt App ở local, outbound từ query DB sẽ rất là nhiều, và chúng ta phải trả với chi phí cao.
- Thay vì đó, chúng ta hãy tạo tất cả các tài nguyên ở trên cloud, khi các dịch vụ giao tiếp với nhau trên môi trường cloud chúng sẽ không mất phí.
- Ngoài ra trong trường hợp này chúng ta có thể sử dụng **Direct Connection** để kết nối từ cloud tới on-premise với chi phí rẻ hơn(cơ mà cái DC này lắp đặt cũng phải hơn tháng mới xong, nên cân nhắc nếu dự án cần sử dụng gấp thì bỏ nha).

