---
layout: post
title: "Bài 5: Giao tiếp HTTP hiện đại với Fetch API trong JS"
---
Fetch API là công cụ tiêu chuẩn để JavaScript giao tiếp với Backend thông qua HTTP.
### **1. Phương thức POST**
Dùng để gửi dữ liệu từ Client lên Server (ví dụ khi đăng ký tài khoản).

### **2. Code ví dụ gửi dữ liệu**
```javascript
const user = { name: "Kiet", job: "Developer" };

fetch('[https://reqres.in/api/users](https://reqres.in/api/users)', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(user)
})
.then(res => res.json())
.then(data => console.log("Kết quả:", data));

### **3. Định dạng JSON**
JSON là ngôn ngữ chung để Java và JavaScript có thể hiểu nhau trong mạng.