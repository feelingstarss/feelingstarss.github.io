---
layout: post
title: "Bài 6: Xây dựng ứng dụng Real-time với WebSocket"
---
WebSocket giữ kết nối luôn mở, cho phép Server chủ động gửi dữ liệu về Client ngay lập tức.
### **1. Khác biệt với HTTP**
HTTP đóng kết nối sau mỗi lần nhận data, còn WebSocket thì không.

### **2. Code Client WebSocket**

```javascript
const socket = new WebSocket('ws://localhost:8080');

socket.onopen = () => {
    socket.send("Chào Server!");
};

socket.onmessage = (event) => {
    console.log("Tin nhắn từ Server:", event.data);
};

```

### **3. Ứng dụng**
Hệ thống chat, thông báo đẩy, cập nhật giá chứng khoán thời gian thực.