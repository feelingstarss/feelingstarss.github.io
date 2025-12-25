---
layout: post
title: "Bài 7: Lập trình TCP Server hiệu năng cao với Node.js"
---
Node.js cực mạnh trong việc xử lý hàng ngàn kết nối đồng thời nhờ cơ chế Non-blocking.
### **1. Module 'net'**
Đây là module cốt lõi để làm việc với các tầng mạng thấp trong Node.js.

### **2. Code Server TCP đơn giản**

```javascript
const net = require('net');

const server = net.createServer((socket) => {
    socket.write('Chào bạn đến với Server!\n');
    socket.on('data', (data) => {
        console.log('Client gửi:', data.toString());
    });
});

server.listen(3000, '127.0.0.1');

### **3. Ưu điểm**
Tốn cực ít RAM so với các mô hình đa luồng truyền thống.