---
layout: post
title: "Bài 6: Làm chủ Fetch API để giao tiếp với Server trong JavaScript"
---
Fetch API là cách hiện đại và sạch sẽ nhất để gửi các yêu cầu HTTP (GET, POST, PUT, DELETE) từ trình duyệt.

Thay vì dùng AJAX cũ kỹ, Fetch API sử dụng Promises giúp code của bạn dễ đọc và bảo trì hơn. Chúng ta sẽ thực hành lấy dữ liệu từ một API công khai và hiển thị kết quả### 6. Bài 6: WebSocket thời gian thực
**File:** `2025-12-06-websocket-realtime.md`
```markdown
---
layout: post
title: "Bài 6: Xây dựng ứng dụng Real-time với WebSocket"
---
Làm sao để tạo ứng dụng Chat mà không cần F5 trang web? Câu trả lời chính là WebSocket.
### 1. Cơ chế hoạt động
Khác với HTTP (đóng sau khi nhận data), WebSocket giữ kết nối luôn mở để hai bên nói chuyện liên tục.

### 2. Code Client đơn giản
```javascript
const socket = new WebSocket('ws://localhost:8080');

socket.onopen = () => {
  socket.send('Chào Server!');
};

socket.onmessage = (event) => {
  console.log('Nhận tin từ Server:', event.data);
}; lên giao diện Blog cá nhân.