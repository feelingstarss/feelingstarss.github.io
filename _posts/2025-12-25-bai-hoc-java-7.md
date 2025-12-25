### 7. Bài 7: Node.js Network Module
**File:** `2025-12-07-node-net-module.md`
```markdown
---
layout: post
title: "Bài 7: Lập trình TCP Server với Node.js"
---
Node.js cung cấp module 'net' giúp bạn tạo Server cực nhanh chỉ với vài dòng code.
### 1. Tại sao chọn Node.js?
Node.js sử dụng cơ chế Non-blocking I/O, cực kỳ phù hợp để xử lý hàng nghìn kết nối mạng đồng thời.

### 2. Code Server TCP
```javascript
const net = require('net');

const server = net.createServer((socket) => {
  socket.write('Chào bạn đã đến với Node.js Server\n');
  socket.pipe(socket); // Echo lại dữ liệu
});

server.listen(1337, '127.0.0.1');