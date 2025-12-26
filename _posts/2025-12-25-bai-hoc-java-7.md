---
layout: post
title:  "Bài 7: Node.js - Khi JavaScript không chỉ nằm trong trình duyệt"
---

Nếu Java là một anh lực sĩ vạm vỡ có thể gánh vác các tác vụ tính toán nặng nề (CPU Intensive), thì Node.js lại là một anh ninja nhanh nhẹn, chuyên xử lý hàng ngàn kết nối nhỏ cùng lúc (I/O Intensive).

Hôm nay, chúng ta sẽ xem xét cách Node.js xử lý TCP Socket khác biệt như thế nào so với Java mà chúng ta đã học ở bài 2.

### 1. Cuộc chiến tư tưởng: Multi-thread vs Event-driven

*   **Java (Multi-thread):** Mỗi khi có khách đến (Client connect), Server tạo ra một Thread mới.
    *   *Ưu điểm:* Dễ tư duy logic.
    *   *Nhược điểm:* Tốn RAM. Nếu có 100.000 khách, Server sẽ sập vì tràn bộ nhớ (mỗi Thread tốn khoảng 1-2MB RAM).

*   **Node.js (Single-thread & Event-driven):** Chỉ có **MỘT** người phục vụ duy nhất.
    *   Cơ chế: "Ai cần gì cứ đăng ký sự kiện, khi nào xong tôi gọi".
    *   *Ưu điểm:* Cực kỳ nhẹ. Một Server Node.js 512MB RAM có thể xử lý hàng chục nghìn kết nối.
    *   *Nhược điểm:* Không giỏi tính toán nặng (Ví dụ: Xử lý video, AI).

### 2. Code Demo: TCP Server siêu tốc với Node.js

Node.js có sẵn module `net` cực mạnh. Bạn không cần cài đặt thư viện bên ngoài nào cả.

Hãy tạo file `server.js`:

```javascript
const net = require('net');

// Danh sách chứa các socket client đang kết nối
const clients = [];

const server = net.createServer((socket) => {
    // 1. Khi có người kết nối
    console.log('Client mới đã kết nối: ' + socket.remoteAddress + ':' + socket.remotePort);
    clients.push(socket);

    socket.write('Chào mừng bạn đến với Server Node.js!\r\n');

    // 2. Khi nhận được dữ liệu
    socket.on('data', (data) => {
        const message = data.toString().trim();
        console.log(`Nhận được: ${message}`);

        // Gửi lại (Echo) cho tất cả mọi người (Giống Chat Server ở Bài 2)
        clients.forEach(client => {
            if (client !== socket) { // Không gửi lại cho chính người gửi
                client.write(`Người lạ nói: ${message}\r\n`);
            }
        });
    });

    // 3. Khi khách tút dây mạng
    socket.on('end', () => {
        console.log('Client đã ngắt kết nối');
        // Xóa client khỏi danh sách (Dùng filter để loại bỏ)
        const index = clients.indexOf(socket);
        if (index > -1) clients.splice(index, 1);
    });
    
    // 4. Xử lý lỗi (Rất quan trọng, không có là crash app)
    socket.on('error', (err) => {
        console.error(`Lỗi Socket: ${err.message}`);
    });
});

// Lắng nghe ở cổng 12345
server.listen(12345, () => {
    console.log('Server Node.js đang chạy tại port 12345...');
});
```

### 3. Cách chạy thử
1.  Cài đặt Node.js (nếu chưa có).
2.  Mở Terminal, gõ: `node server.js`
3.  **Điều thú vị:** Bạn hoàn toàn có thể dùng **Java Client** (ở Bài 2) để kết nối vào **Node.js Server** này!
    *   *Vì sao?* Vì cả hai đều nói chung một ngôn ngữ là **Giao thức TCP**. Đừng quan trọng ngôn ngữ lập trình là gì, miễn là tuân thủ giao thức mạng chuẩn.

### 4. Kết luận
Node.js sinh ra là để làm mạng. Cú pháp đơn giản, hiệu năng cao cho các ứng dụng real-time. Tuy nhiên, đừng thần thánh hóa nó. Nếu bạn cần làm một hệ thống ngân hàng cần tính toán giao dịch phức tạp và an toàn kiểu dữ liệu chặt chẽ, Java vẫn là lựa chọn số 1.

Ở **Bài 8**, chúng ta sẽ nói về một chủ đề "khô khan" nhưng cực kỳ quan trọng: **Bảo mật**. Làm sao để người khác không đọc trộm tin nhắn của bạn trên đường truyền?