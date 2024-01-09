---
quickshare-date: 2024-02-20 14:37:28
quickshare-url: "https://noteshare.space/note/clsu1yzj45566501mw1x4zaa0u#Bp80k/xOzchTMR9g792d8rD3KTNi8N3X7DqnknbPjaA"
---
# 1. Task#27 Hiển thị route BT -> CT trên achievement detail.
- Mục tiêu:
	- Trên màn achievement detail chỉ hiển thị route từ CT -> BT. Expect: hiển thị cả route từ BT về công trường.
	- Thay đổi cách tính thời điểm ra vào CT-BT trên report detail
	- Thay đổi vị trí hiển thị CT và BT. Logic hiện tại đang lấy lệch vị trí so với CT và BT thực tế do logic lấy sau khoảng thời gian(2p hoặc 30s).
![[00 Meta/01 Attachments/Pasted image 20240220095243.png]]

### Yêu cầu:
- [ ] Vẽ route từ BT -> CT
	- Điều kiện: Achivement mới(achievement được tạo ngay sau achievement đang xét) có cùng CT, và chung project.

- [ ] Logic cũ không thay đổi, chỉ thay đổi thời điểm lấy tọa độ vẽ CT và BT trên màn achievement detail.
- [ ] Sửa thời ra -> thời gian vào trên màn report detail.

### Câu hỏi
- ![[00 Meta/01 Attachments/Pasted image 20240220145506.png]] không hiểu.
# 2. Bổ sung tính năng gửi SMS.
- Mục tiêu: gửi SMS khi driver vào CT cho SĐT của project cha và project current.
### Yêu cầu
- [ ] Nếu project cha và con trùng số đt -> send duplicate sms.(sửa nội dung sms không nằm trong scope)
# 3. Hiển thị route CT->BT trên modal chỉ định route.
- Mục tiêu: confirming

# 4. Thay đổi cách hiển thị và phạm vi của trạng thái hoạt động
- Mục tiêu: Thay đổi logic hiển thị trên màn map, thông tin của driver, hiển thị CT và BT lên map.

### Yêu cầu
- [ ] Default: display icon mũi tên driver + popup-min với thông tin số xe + driver. Icon CT + BT.
- [ ] Default: Bounder tất cả các icon(driver + CT + BT).
- [ ] Thêm button hiển thị Toàn bộ thông tin
	- ON -> Hiển thị popup
	- OFF -> Ẩn tất cả popup
- [ ] Click vào driver(trên list driver/icon/popup): không thay đổi size popup + centering icon.
- [ ] Trên popup: vẫn có button maximal/minimal popup.
- [ ] Click icon CT/BT: hiển thị popup.
	- Popup cũng có button maximal/minimal.
- [ ] Toggle popup ẩn/hiện khi click icon CT/BT.
- [ ] Hiển thị toàn bộ icon CT/BT, màu của icon lần lượt xoay vòng theo sắp xếp [thứ tự ở đây](https://docs.google.com/presentation/d/1BYFwkZw9l_ki0y-_JRXkGEq7bvW5lidp/edit#slide=id.p12).
	- Điều kiện hiển thị CT/BT:
		- Confirm: Chỉ hiển thị CT và BT theo project tồn tại trong ngày phải không? 
		- Chỉ có CT hoặc BT gắn với project thì cũng hiển thị icon lên map.
	- Hiển thị màu:
		- CT và BT trong cùng project hiển thị **cùng màu**.
- [ ] Bỏ button **toggle button 大/小**

### Câu hỏi:
1. ![[00 Meta/01 Attachments/Pasted image 20240220133242.png]] - Bound tất cả icon nằm trong khu vực Nhật Bản. Ngoài Nhật, có hiển thị icon nhưng ko bound.
2. ![[00 Meta/01 Attachments/Pasted image 20240220134943.png]] Không hiểu ý 7.
3. Điều kiện hiển thị icon CT/BT: Chỉ hiển thị CT và BT theo project tồn tại trong ngày phải không?
4. Màu của icon CT/BT: Nếu có nhiều hơn 12 cặp icon CT/BT thì hiển thị lại màu lại từ đầu theo thứ tự hay cần xin thêm màu của khách?
5. Hiện tại mình chưa có icon bãi đậu xe.