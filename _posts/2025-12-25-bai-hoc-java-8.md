---
layout: post
title:  "Bài 8: Đừng để Hacker đọc trộm tin nhắn của bạn!"
date:   2025-12-26 08:00:00 +0700
---

Trong 7 bài trước, chúng ta chỉ quan tâm đến việc làm sao để code "chạy được". Nhưng trong thực tế, code chạy được mà không bảo mật thì thà đừng viết còn hơn.

Hôm nay, chúng ta sẽ bàn về **Network Security** (Bảo mật mạng) - lá chắn duy nhất bảo vệ người dùng của bạn.

### **1. Tấn công Man-in-the-Middle (MITM) là gì?**

Hãy tưởng tượng bạn (A) đang gửi thư tình cho cô ấy (B) trong lớp học. Bạn nhờ thằng bạn cùng bàn (C) chuyền thư giúp.
*   **Kịch bản không an toàn (HTTP):** Bạn đưa thư không dán tem. Thằng C mở ra đọc trộm ("À há, thằng này thích con B"), thậm chí nó có thể sửa nội dung thư thành "Tao ghét mày" rồi mới đưa cho B. -> Toang!
*   **Kịch bản an toàn (HTTPS):** Bạn viết thư bằng mật mã chỉ bạn và cô ấy hiểu. Thằng C cầm thư nhưng chỉ thấy những ký tự vô nghĩa. Nó cũng không thể sửa thư vì sửa xong nội dung sẽ trở thành rác không đọc được.

Internet cũng vậy. Khi bạn ngồi quán Cafe Public Wifi, Hacker có thể ngồi ngay bàn bên cạnh và bắt toàn bộ gói tin bạn gửi đi. Nếu bạn dùng HTTP thường, hắn sẽ thấy hết mật khẩu, số thẻ tín dụng của bạn.

### **2. HTTPS và TLS Handshake**
Để chống lại MITM, thế giới tạo ra **HTTPS** (Hypertext Transfer Protocol Secure). Chữ **S** ở cuối là phép màu.

Cơ chế hoạt động (Đơn giản hóa):
1.  **Client:** "Chào Server, tôi muốn kết nối bảo mật."
2.  **Server:** "Ok, đây là 'Chứng minh nhân dân' (Certificate) và Khóa Công Khai (Public Key) của tôi."
3.  **Client:** Kiểm tra xem CMND có phải đồ giả không nhờ vào bên thứ 3 uy tín (CA - Certificate Authority). Nếu OK, Client tạo ra một khóa bí mật, mã hóa nó bằng Public Key của Server rồi gửi lại.
4.  **Server:** Dùng Khóa Riêng (Private Key) để giải mã và lấy được khóa bí mật.
5.  **Kết nối thiết lập:** Từ giờ cả hai dùng khóa bí mật chung đó để nói chuyện. Bố ai mà nghe lén được nữa!

### **3. Nguyên tắc vàng: "Never Trust User Input"**

Đừng bao giờ tin tưởng dữ liệu người dùng gửi lên. Hacker luôn tìm cách chèn mã độc vào các ô Input.

#### Lỗi 1: SQL Injection (Tiêm thuốc độc vào Database)
Code ngây thơ:
```java
String query = "SELECT * FROM users WHERE name = '" + userName + "'";
```
Hacker nhập vào ô tên: `Kiet' OR '1'='1`
Câu lệnh trở thành: `SELECT * FROM users WHERE name = 'Kiet' OR '1'='1'`
-> Vì `'1'='1'` luôn đúng, Hacker đăng nhập được vào bất kỳ tài khoản nào mà không cần mật khẩu!

**Cách phòng chống:** Luôn dùng **Prepared Statement** (có dấu `?`).
```java
String query = "SELECT * FROM users WHERE name = ?";
pstmt.setString(1, userName); // An toàn tuyệt đối
```

#### Lỗi 2: XSS (Cross-Site Scripting)
Hacker nhập vào ô bình luận: `<script>alert('Mày bị hack!')</script>`
Nếu bạn hiển thị nguyên văn nội dung này lên web, trình duyệt của người xem khác sẽ chạy đoạn code JS đó. Hacker có thể dùng nó để ăn cắp Cookie, Token của người dùng khác.

**Cách phòng chống:** Luôn **Escape** dữ liệu trước khi hiển thị (Biến `<` thành `&lt;`, `>` thành `&gt;`). Các Framework hiện đại (React, Angular...) thường làm sẵn việc này giúp bạn.

---
Ở **Bài cuối cùng (Bài 9)**, chúng ta sẽ tổng kết lại hành trình và vẽ ra một tấm bản đồ (Roadmap) để bạn biết mình cần đi đâu tiếp theo: Microservices hay Cloud?