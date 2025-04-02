---
title: 🌱 Antidetect là gì?
tags:
  - til
  - antidetect
date: 2025-04-02
aliases:
  - antidetect
draft: false
---
# 🌿 What?
Là kỹ thuật sử dụng công cụ để ẩn dấu vết kỹ thuật số của người dùng, chẳng hạn như trình duyệt, IP, cookie, fingerprint, thiết bị, ... nhằm tránh bị phát hiện hoặc theo dõi bởi các hệ thống nhận dạng.

# 🌿  How?
## Browser Fingerprinting - Vân tay trình duyệt
- Là kỹ thuật thay đổi các yếu tố như User-Agent, WebGL, Canvas, fonts, timezone, screen resolution, audio context, ...

## Proxy và VPN
- Đổi IP giúp người dùng giả lập đang ở nơi khác

## Isolation - Cô lập
- Các profiles của các trình duyệt được cô lập để tránh cookie + các thông tin khác liên kết với nhau.

# 🚫 Các biện pháp chống Antidetect
- Các dịch vụ lớn ngày càng thông minh, sử dụng Machine Learning, AI để phân thích các hành vi bất thường, hoặc so sánh tính nhất quán giữa IP, [[50 til/51 Code/13 Antidetect/Browser Fingerprint|Browser fingerprint]] và hành vi người dùng.
- Ví dụ: Timezone ở VN nhưng IP ở Mỹ, font chữ chỉ có trên Windows lại có trên máy Mac, hay tốc độ nhập chữ nhanh bất thường, ....

# Refer
https://detect.expert/vi/blog/