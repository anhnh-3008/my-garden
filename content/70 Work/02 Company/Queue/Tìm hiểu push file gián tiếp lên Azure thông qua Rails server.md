---
title: Tìm hiểu push file gián tiếp lên Azure thông qua Rails server
date: 2023-10-05
draft: true
---
#### Upload ✅
- Upload lên folder /storage trên server
- Từ server đẩy file lên Azure - Viết một method callback khi ActiveStorage:Attachment được tạo.
- Cần xoá file trong /storage sau khi đã upload lên Azure : 🚫 không cần, luồng hiện tại đang không xoá file trên Azure. - **Đề xuất**

- ❓Làm sao để giữ relation của ActiveStorage
	- Luồng vẫn giữ nguyên như cũ, ActiveStorage vẫn sẽ tạo record cho Blob và Attachment.

- Viết callback xác định khi có một ActiveStorage Attachment record được tạo mới, thực hiện đẩy lên Azure.
- ❓Viết callback vào đâu, nếu tạo một file model ActiveStorage::Attachment sẽ phải đảm bảo giữ nguyên logic của model
	- Nếu copy code từ bên repo Rails -> Sau này khi rails cập nhật thêm vào model ActiveStorage::Attachment sẽ bị miss. 🚫
	- Viết callback vào model Project, viết vào after_save, thử file_attachment_changed? xem có được ko.
#### Load ✅
- Không cần quan tâm, do hệ thống không có đọc content, chỉ có download.
#### Download 🚧
- Download từ Azure 
#### Delete ✅
-  Xoá thì chỉ xoá relationship, file trên Azure vẫn giữ nguyên(luồng hiện tại đang thực hiện như vậy)
- Blob cũng không được xoá khi một Attachment liên kết bị xoá


#### Vấn đề
- [ ] Cải thiện tốc độ download file
	- Tìm hiểu trong lib `/Users/nguyen.hoang.anhc/.rbenv/versions/2.7.1/lib/ruby/gems/2.7.0/gems/railties-6.0.4.7/lib/activestorage`
- [ ] Viết Unit test
	- [ ] Service push file
	- [ ] Service get content
	- [ ] Worker
	- [ ] Callback of project after validation
	- [ ] Rake task remove file in /storage
ActiveRecord::Schema.define(version: 2023_10_11_095052) do
t.boolean "uploaded", default: false