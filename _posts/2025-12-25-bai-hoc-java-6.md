---
layout: post
title:  "Bài 6: WebSocket - Vũ khí tối thượng cho ứng dụng Real-time"
---

Hãy tưởng tượng bạn đang vào Facebook. Ai đó comment vào ảnh của bạn, thông báo hiện lên **ngay lập tức** mà bạn không cần tải lại trang. Magic? Không, đó là **WebSocket**.

### **1. HTTP vs WebSocket: Khác nhau chỗ nào?**

*   **HTTP (Truyền thống):**
    *   Client: "Có tin nhắn mới không?" -> Server: "Không". (Đóng kết nối)
    *   1 giây sau... Client: "Có tin mới không?" -> Server: "Không".
    *   Cực kỳ tốn tài nguyên và chậm (Polling).

*   **WebSocket (Hiện đại):**
    *   Client: "Alo Server, thông đường ống nước nhé!" (Handshake).
    *   Kết nối **MỞ LIÊN TỤC**.
    *   Khi có tin mới, Server tự động **BƠM** thẳng về Client ngay lập tức. Cả hai bên có thể nói chuyện bất cứ lúc nào (Full-duplex).

### **2. Code Demo: Chat Server "Echo"** 

Để đơn giản, chúng ta sẽ dùng một Server test công cộng là `wss://echo.websocket.events`. Server này có nhiệm vụ: Bạn gửi cái gì lên, nó sẽ trả về y hệt cái đó (như tiếng vọng).

Bạn hãy tạo một file `index.html` và copy đoạn code này vào chạy thử nhé:

```html
<!DOCTYPE html>
<html>
<head>
    <title>WebSocket Demo</title>
    <style>
        body { font-family: sans-serif; padding: 20px; }
        #messages { border: 1px solid #ccc; height: 300px; overflow-y: scroll; padding: 10px; margin-bottom: 10px;}
        .my-msg { color: blue; text-align: right; }
        .server-msg { color: green; text-align: left; }
    </style>
</head>
<body>
    <h2>Phòng Chat WebSocket</h2>
    <div id="status">Trạng thái: Đang kết nối...</div>
    <div id="messages"></div>
    
    <input type="text" id="inputMsg" placeholder="Nhập tin nhắn..." style="width: 70%;">
    <button onclick="guiTin()">Gửi</button>

    <script>
        // 1. Khởi tạo kết nối tới Server
        const socket = new WebSocket('wss://echo.websocket.events');
        
        const statusDiv = document.getElementById('status');
        const msgDiv = document.getElementById('messages');

        // 2. Sự kiện: Khi kết nối thành công
        socket.onopen = function(event) {
            statusDiv.innerHTML = "Trạng thái: <b style='color:green'>Đã kết nối!</b>";
            statusDiv.innerHTML += "<br>Server này sẽ tự động trả lời lại những gì bạn chat.";
        };

        // 3. Sự kiện: Khi nhận được tin nhắn từ Server
        socket.onmessage = function(event) {
            console.log("Server gửi về:", event.data);
            hienThiTinNhan("Server: " + event.data, 'server-msg');
        };

        // 4. Sự kiện: Khi mất kết nối
        socket.onclose = function(event) {
            statusDiv.innerHTML = "Trạng thái: <b style='color:red'>Mất kết nối!</b>";
        };

        // Hàm gửi tin nhắn
        function guiTin() {
            const input = document.getElementById('inputMsg');
            const tinNhan = input.value;
            
            if (tinNhan.trim() !== "") {
                // Gửi dữ liệu lên Server
                socket.send(tinNhan); 
                
                hienThiTinNhan("Bạn: " + tinNhan, 'my-msg');
                input.value = ""; // Xóa ô nhập
            }
        }

        function hienThiTinNhan(noidung, cssClass) {
            const p = document.createElement('div');
            p.innerText = noidung;
            p.className = cssClass;
            msgDiv.appendChild(p);
            msgDiv.scrollTop = msgDiv.scrollHeight; // Tự cuộn xuống dưới cùng
        }
    </script>
</body>
</html>
```

### **3. Những lưu ý sống còn khi làm Real-time**

1.  **Mất kết nối (Reconnection):** Wifi người dùng có thể chập chờn. Bạn phải viết code tự động kết nối lại (Auto-reconnect) nếu bị ngắt.
    ```javascript
    socket.onclose = function() {
        console.log("Rớt mạng! Đang thử kết nối lại sau 3s...");
        setTimeout(connectWebSocket, 3000); // Gọi hàm đệ quy để kết nối lại
    }
    ```

2.  **Heartbeat (Nhịp tim):** Một số Router mạng sẽ tự cắt kết nối nếu thấy "im lặng" quá lâu.
    *   Giải pháp: Cứ 30 giây, Client gửi một tin nhắn rỗng (Ping) lên Server, Server trả lời (Pong) để báo hiệu "Tao vẫn còn sống, đừng cắt mạng tao".

3.  **Bảo mật:** Luôn dùng `wss://` (WebSocket Secure) thay vì `ws://` để mã hóa dữ liệu, tương tự HTTPS.

Ở **Bài 7**, chúng ta sẽ đổi gió một chút. Thay vì dùng Java làm Server, chúng ta sẽ thử dùng **Node.js** - nền tảng sinh ra để làm việc với mạng - để xem nó bá đạo như thế nào!