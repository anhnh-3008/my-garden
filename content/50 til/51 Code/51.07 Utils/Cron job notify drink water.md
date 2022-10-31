---
title: "🥂 Tạo background job nhắc nhở uống nước đều đặn"
tags: [til, script, cron job]
date: 2022-10-02
---

---
Không biết mọi người có giống mình không, mỗi khi làm việc mình cứ bị quên uống nước ấy, có khi cả buổi mình còn chả uống được 250ml nước =((. Tác hại của việc uống ít nước mọi người có thể gg nha, nhưng ncl uống nước đủ mỗi ngày là thói quen rất có lợi cho sức khỏe cũng như làn da của chúng ta =)).

Hôm trước mình có gặp anh mentor ở cty, anh ấy chia sẻ là vì hay ngồi gù lưng nên anh ấy viết một script để sau một khoảng thời gian, thông báo kiểu như 'Thẳng lưng lên!' được hiển thị trên Touch Bar. 🤩, hay thế!!! Sao mình ko áp dụng để improve khả năng uống nước của bản thân nhỉ 🤔 Thế nên tranh thủ cuối tuần, mình có tìm cách để setup cronjob cho Ubuntu.

🌱 Đầu tiên là setup cronjob, mình có xài `cron`, mn có thể dùng apt để install và enable nó lên nhé.
```sh
sudo apt update
# Check if cron package is installed
dpkg -l cron

# install cron
sudo apt install cron

# enable cron
systemctl start cron

# check status cron
systemctl status cron

# stop cron
systemctl stop cron
```

🌱 Để thêm job, sử dụng command:
```sh
crontab -e
```

Trong file đã có hướng dẫn cụ thể, về cơ bản cũng giống như setup cron-sidekiq, nếu chưa quen settings thời gian chạy job mọi người có thể sử dụng [cron-time](https://crontab.guru/) cho trực quan nhé!

Ví dụ mình set 20p là phải nhắc t uống nước đó nha Ubuntu =))
```sh
20 * * * * cd ~/personal && ./script-notify-myself.sh
```

🌱 Tạo script:
```sh
#!/bin/bash

export DBUS_SESSION_BUS_ADDRESS="${DBUS_SESSION_BUS_ADDRESS:-unix:path=/run/user/${UID}/bus}"
notify-send "Uống nước đii!!!"
```

🌱 Và kết quả là:
**![](https://lh5.googleusercontent.com/0NKuSVNogMqGwdDajpn-B901GQITiJWGHqrWUFlI6FYn20D7eaE3DbcREvNv-bBYiwZQvJxaC0GuQry-tXdIIWbm-VG9WpXql-A8pr8ZzybJRR0q62qFrfVKmioH9AHzGqZ6oES1olMjkKRUNN18liShoJREFpkd9EflllQjAGoJW2D1EJkM3WBI0A)**


### 🌱 Update
---
Sau một thời gian thêm cronjob, mình khá là khó chịu vì cái bảng thông báo của mình nó cứ hiển thị chất đống `Uống nước đii!!!`, rất là mất mỹ quan đô thị.

![[00 Meta/01 Attachments/Notifi Trash.png]]

Để khắc phục vấn đề này, mình có thêm một script chịu trách nhiệm để clear-all tất cả những thông báo hiện tại. 

```sh
# ./remove-all-notify-tray.sh

#!/bin/bash
gdbus call --session --dest org.gnome.Shell --object-path /org/gnome/Shell --method org.gnome.Shell.Eval 'Main.panel.statusArea.dateMenu._messageList._notificationSection._list.remove_all_children()'
```

🌱 Mình có viết scripts ở [đây](https://github.com/anhnh-3008/dotfiles/tree/main/cronjob)  để sau dụng lại cho tiện, nếu thấy hứng thú mọi người có thể pull về chạy thử nha ❤️
