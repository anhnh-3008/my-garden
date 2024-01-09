---
title: "🌱 Solution Architect Discussion - Whattimeisit.com"
tags: [aws, architecture]
date: 2023-03-12
---

- Đề bài: Tôi cần build kiến trúc cho một web xem thời gian, có domain là **whattimeisit.com**

1. Đây là một app hỏi giờ thôi nên không cần database để lưu dữ liệu. Đầu tiên tôi cần launch một EC2 Instance + ElasticIP để người dùng có thể truy cập để hỏi giờ.
![[00 Meta/01 Attachments/Pasted image 20230312115417.png]]

2. Sau đó, app được người dùng trải nghiệm tốt, họ giới thiệu cho bạn bè, một vài người sử dụng thử và lượng truy cập tăng lên. Tôi cần phải năng cấp Instance để đáp ứng nhu cầu sử dụng, lúc đầu là T2 -> M5.
	1. Stop Instance đang chạy
	2. Đổi thủ công từ T2 -M5
	3. Lauch lại Instance, vì sử dụng Elastic IP nên không ảnh hướng đến địa chỉ truy cập.
![[00 Meta/01 Attachments/Pasted image 20230312121026.png]]
- Trong thời gian upgrade, người dùng không thể truy cập để hỏi giờ được, thời gian downtime sẽ ảnh hưởng đến trải nghiệm của người dùng. Nhưng vì giờ app nó vẫn còn nhỏ, nên thôi cứ dùng tạm vậy đã.

3. Sau đó app thật sự nổi tiếng, lượng truy cập ồ ạt, tiếp theo tôi sẽ thực hiện scaling horizontal.
![[00 Meta/01 Attachments/Pasted image 20230312165841.png]]

4. Vấn đề là người dùng sẽ phải nhớ địa chỉ IP tương ứng với từng instance để truy cập, về sau càng scale lên càng nhiều instances, việc nhớ IPs là rất bất tiện. Để giải quyết vấn đề này, tôi sử dụng **Route 53** để điều hướng địa chỉ IP cho người dùng. 
![[00 Meta/01 Attachments/Pasted image 20230312171324.png]]

5. Nhưng hiện tại, nhu cầu scale là thường xuyên, việc add instance thêm hoặc đặc biệt là remove sẽ gây bất tiện. Do TTL được set là 1 giờ, nếu instance bị xóa thì trong một giờ nhóm user có response DNS sẽ không thể sử dụng được app, ảnh hưởng đến trải nghiệm. Ở bước này, tôi đầu tư thêm tiền để thực hiện scale horizontal bằng **ELS - Elastic Load Balancer**.
	- Vì ELB sẽ có IP thay đổi nên tôi bật alias trong DNS record lên, trỏ về ELB.
6. Cơ mà thấy phải scale thủ công cũng hơi bất tiện, thế là tôi dùng thêm dịch vụ **ASG - Auto Scaling Group** để tự động scale.
7. Bật thêm **Multi-AZ** để phòng tránh trường hợp bất ngờ như động đất sóng thần gì đấy làm hỏng một AZ, các AZ còn lại sẽ vẫn hoạt động bình thường.
8. Ok, giờ thì optimize cost một chút, tôi biết rằng chắc chắn mỗi năm sẽ cần ít nhất 2 instances để chạy app, tôi sẽ lựa chọn option **reserved instance** để thuê 2 instances cho 2 AZs, còn lại phát sinh tôi sẽ dùng option **spot instances** để tiết kiệm chi phí.

> [!note] Summary
> 
> Các bước bên trên là các bước để tạo nên một kiến trúc tốt trên nền tảng AWS, nó bao gồm 5/6 trụ cột
> 1. operation pillar - vận hành tốt, đáp ứng nhu cầu mở rộng tự động và hợp lý cho hệ thống
> 2. reliability pillar - uy tín, luôn định tuyến tới các healthy instance cũng như có dự phòng ngay khi xảy ra lỗi.
> 3. performance pillar - đáp ứng khả năng xử lý, tính toán tốt cho hệ thống
> 4. security pillar - các rules được thiết lập chặt chẽ, các requests sẽ được đi qua đúng các điểm chỉ định để đảm bảo tính an toàn cho hệ thống.
> 5. optimize cost pilllar - chi phí sử dụng được tối ưu với những options của các dịch vụ phù hợp với nhu cầu sử dụng của ứng dụng.



