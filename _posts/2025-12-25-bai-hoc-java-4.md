---
layout: post
title: "Bài 4: JavaScript và sức mạnh của lập trình bất đồng bộ"
---
Trong mạng, việc chờ dữ liệu không được làm nghẽn ứng dụng. JavaScript giải quyết bằng Async/Await.
### **1. Khái niệm Async/Await**
Giúp code bất đồng bộ trông giống như code chạy tuần tự, dễ đọc và dễ bảo trì hơn.

### **2. Code minh họa**

```javascript
async function layDuLieu() {
    console.log("Bắt đầu lấy dữ liệu...");
    try {
        const response = await fetch('[https://api.github.com/users](https://api.github.com/users)');
        const data = await response.json();
        console.log("Dữ liệu nhận được:", data.length);
    } catch (err) {
        console.error("Lỗi mạng:", err);
    }
}

layDuLieu();

### **3. Lợi ích**
Ứng dụng web vẫn mượt mà trong khi dữ liệu đang được tải từ Server.