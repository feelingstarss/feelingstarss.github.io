---
layout: post
title: "Bài 5: Giao tiếp HTTP hiện đại với Fetch API"
---
Fetch API là công cụ chuẩn để JavaScript giao tiếp với Server thông qua các HTTP Request.
### 1. Các phương thức phổ biến
- **GET:** Lấy dữ liệu.
- **POST:** Gửi dữ liệu mới lên Server.

### 2. Ví dụ gửi dữ liệu (POST)
```javascript
fetch('[https://api.example.com/posts](https://api.example.com/posts)', {
  method: 'POST',
  body: JSON.stringify({ title: 'Đồ án', content: 'Lập trình mạng' }),
  headers: { 'Content-type': 'application/json' }
});