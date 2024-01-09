---
quickshare-date: 2024-02-22 23:53:50
quickshare-url: "https://noteshare.space/note/clsxgq6ei6188901mwvttmn3bk#h13tY9Va5v5+pbhejMz/6tgKEZpJm06V7WrmDdcjFjs"
---
## Posts
- [x] Get Top List API
- [x] Get Blog List API
- [x] Get Listing List API
- [x] Get Video List API
- [x] Get Detail Post API
- [x] Like Post API
- [x] Save Post API
- [ ] Get Houses API
- [ ] Flagging content as not interested API
- [ ] Blur thumbnail for sensitive content
- [ ] Report Post API
## Comments
- [x] Get Comment List by Post API
- [x] Create Comment API
- [x] Reply Comment API
- [x] Like Comment API
- [x] Dislike Comment API
- [ ] Report Comment API

## Search Posts
- [x] Search API

> [!note] Note
> Những API chưa tích là chưa có code, nhờ em confirm với khách xem những API này có nằm trong scope không? để bên mình xử lý nhé

### Logic check Permission
- Logic này để check xem user sẽ có thể xem được những posts nào? và đọc được những comments nào?
- Logic hiện tại đang được implement:
	- Privacy là Everyone.
	- Nếu privacy là Friend, thì phải nằm trong danh sách follower or following.
	- Không xem được với các post privacy là OnlyMe.

> [!question] QA
> Logic check Permission có cần thêm điều kiện không hiển thị bài post mà người dùng đã report trước đây ko?