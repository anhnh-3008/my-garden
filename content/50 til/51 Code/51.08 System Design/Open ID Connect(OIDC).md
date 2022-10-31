---
title: "🔐 Open ID Connect(OIDC)"
tags: [til, sys design, security]
date: 2022-09-28
---

---

Là một loại cơ chế xác thực kiểu [[50 til/51 Code/51.08 System Design/Single Sign-On(SSO)]] dựa trên thuật toán **mật mã hóa khóa bất đối xứng**. Có 2 khóa đảm nhiệm riêng từng nhiệm vụ là mã hóa và giải mã.
**![](https://lh5.googleusercontent.com/1cxM7BkCmyzrm0Q17OIv7x3GcMzfyLhaHnExHl6foJLIL0e0nruB8tWPJu4RwoZNlLn1XFNlieM0gG2JiCHff760sQ87LyzxX1GJobxyoPGE0i72olWaxzLasNXmm3_iC4NEYfsKheuPVME_LxigUMArWVomwIKfbCD1Gt82o_Hs3Vh2d_HKWweu3A)**
**![](https://lh4.googleusercontent.com/ku-PU5gsE-WnRbitam-zVKFWzcmYPxsst_bfbtVlU3KhmKcIbJ9qB5-TVBnoxQHkOfWRWEVLmV_fwQk7lgiU_t8-UYHti_T4ZBSXxh3k-Ei_2Gm_oufq8LKosdEVYrjenxEnkzPqNYCKAA_3vggJT2XeD8_Rj_ud8g6gNCTWO_0qtfKY_kfMFiD66g)**

Ảnh trên mô tả cơ chế hoạt động của [Mật mã hóa khóa công khai](https://vi.wikipedia.org/wiki/M%E1%BA%ADt_m%C3%A3_h%C3%B3a_kh%C3%B3a_c%C3%B4ng_khai), hiểu đơn giản thì 2 cái này sẽ giống nhau nhưng với 1 cái thì cả 2 khóa phải được giữ bí mật còn lại thì một khóa bí mật một khóa công khai.

OIDC là phiên bản mở rộng của Oauth 2.0, thay vì là Access-Token chúng ta sẽ nhận được một Id Token từ Auth Server. Với [access-token](https://oauth.net/id-tokens-vs-access-tokens/#:~:text=Access%20tokens%20are%20what%20the,read%20by%20the%20OAuth%20client.), mỗi lần qua một trang web khác chúng ta sẽ cần request lại access-token mới nhưng với id-token có thể dùng lại thoải mái, [id-token](https://oauth.net/id-tokens-vs-access-tokens/#:~:text=Access%20tokens%20are%20what%20the,read%20by%20the%20OAuth%20client.) có thể xác thực được user cũng như đảm bảo được các thông tin thuộc về User là ko thể bị giả mạo.
