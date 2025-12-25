---
layout: post
title: "Bài 8: Các nguyên tắc bảo mật cốt lõi khi lập trình mạng"
---
Mạng internet chứa đựng nhiều rủi ro, bảo mật dữ liệu là yếu tố sống còn của ứng dụng.
### **1. HTTPS và mã hóa**
Luôn sử dụng SSL/TLS để mã hóa đường truyền giữa Client và Server.

### **2. Ví dụ Code kiểm tra sơ bộ**

```javascript
function xuLyDuLieu(input) {
    if (typeof input !== 'string') {
        return "Dữ liệu không hợp lệ!";
    }
    console.log("Dữ liệu hợp lệ: " + input);
}

### **4. Kết luận**
Bảo mật tốt giúp bảo vệ uy tín và thông tin của người dùng.