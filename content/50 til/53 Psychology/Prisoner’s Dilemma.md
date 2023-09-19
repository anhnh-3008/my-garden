---
title: "🌱 Prisoner’s Dilemma"
tags: [til, game_theory]
date: 2023-02-03
---

# 🌿 What?

![[00 Meta/01 Attachments/Pasted image 20230203171527.png]]

- 🌱 Prisoner’s Dilemma - Thế lưỡng nan của tù nhân là một thuyết trò chơi(game theory) dùng để nghiên cứu hành vi hợp tác của con người.
- 🌱 Luật chơi đơn giản như sau: Có 2 người A và B cùng bị bắt vì tình nghi là băng cướp ngân hàng(do cảnh sát phát hiện 2 người họ có súng). Có 3 TH có thể xảy ra:
	1. Nếu cả 2 cùng thú tội thì mỗi người sẽ ngồi tù 5 năm.
	2. Nếu cả 2 cùng im lặng thì mỗi người sẽ chỉ ngồi tù 1 năm do tàng trữ vũ khí trái phép.
	3. Nếu B khai báo và A im lặng thì B sẽ được thả còn A sẽ ngồi tù 20 năm và ngược lại.
- 🌱 Đứng từ góc nhìn của A, nếu A im lặng thì ít nhất sẽ ngồi tù 1 năm, có thể là 20 năm nếu B khai báo. Còn khi A khai báo có thể sẽ được thả hoặc nhiều nhất chỉ phải ngồi tù 5 năm. -> Vậy chọn khai báo vẫn là có lợi hơn đúng không?
- 🌱 Có thể thấy trong trò chơi này, nếu là A, bất kể B có chọn phương án nào, việc chọn **khai báo** sẽ mang lại kết quả **có vẻ tốt hơn** cho bản thân. Và đương nhiên B cũng sẽ nghĩ như vậy -> Với sự lựa chọn ích kỉ, cuối cùng thì mỗi người nhận 5 năm tù và đây không phải là kết quả **tốt nhất** mà cả 2 bên có thể đạt được.

> [!note] Note
> 
> Trong một nhóm, hợp tác sẽ mang lại lợi ích tổng thể tốt nhất cho tất cả. Tuy nhiên nó chỉ có thể tồn tại dựa trên sự tin tưởng và cùng hướng về lợi ích chung.
> 

- 🌱 Thuyết trò chơi này được dùng để nghiên cứu những quyết định liên quan đến lợi ích của những cá nhân hoặc tổ chức với nhau. Được áp dụng cho nhiều lĩnh vực như kinh tế, khoa học chính trị, tâm lý, ...
- 🌱 Ví dụ như thực tế trong lĩnh vực kinh doanh, thuyết sẽ được sử dụng để phân tích khả năng cạnh tranh thị trường, chiến lượng định giá sản phẩm hoặc hành vi của những doanh nghiệp có thị trường độc quyền. 
- 🌱 Năm 1980, Robert Axerold, một giáo sư chính trị trường đại học Michigan mời 14 nhà toán học và kinh tế học để chơi Prisoner’s Dilemma, mục đích để tìm ra chiến lược tốt nhất.  Kết quả là chiến thuật đơn giản của giáo sư Anatol Rapoport từ Đại học Toronto, Canada, đã dành được số điểm cao nhất. Chiến thuật tên là **ăn miếng trả miếng(Tit For Tat)**, bao gồm 2 nguyên tắc:
	1. Lượt đầu chọn hợp tác.
	2. Từ lượt sau chọn giống như đối thủ đã chọn ở lượt trước.

> [!note]  Kết luận rút ra từ chiến thuật trên
> 
> - Luôn hợp tác đầu tiên.
> - Tự vệ nhưng biết tha thứ(phản công khi đối thủ không hợp tác, hợp tác khi đối thủ hợp tác lại)
> - Luôn duy trì hợp tác(không đố kị hay để lợi ích cá nhân tác động).
> - Luôn phải nhớ, đối tác(đối thủ) cũng nắm được luật chơi.

- 🌱 Ngoài ra mọi người có thể chơi thử game [The evolution of Trust](https://github.com/ncase/trust) để có cái nhìn trực quan hơn về vấn đề này nhé.

# 🌿 Refer 
- https://vi.wikipedia.org/wiki/Song_%C4%91%E1%BB%81_t%C3%B9_nh%C3%A2n