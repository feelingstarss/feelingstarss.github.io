---
layout: post
title: "Bài 8: Bảo mật dữ liệu trong truyền tải mạng"
---
Đừng để lộ thông tin người dùng! Hãy tìm hiểu về SSL/TLS và mã hóa dữ liệu.
### 1. Các nguy cơ tiềm ẩn
- Đánh cắp gói tin (Sniffing).
- Tấn công giả mạo (Spoofing).

### 2. Giải pháp cơ bản
- Luôn sử dụng **HTTPS** thay vì HTTP.
- Mã hóa mật khẩu bằng các thuật toán như BCrypt trước khi lưu.

### 3. Ví dụ mã hóa đơn giản (Java)
Luôn dùng các thư viện bảo mật tiêu chuẩn, không nên tự viết lại thuật toán mã hóa riêng.