---
layout: post
title:  "Bài 2: Tự tay viết ứng dụng Chat với Java Socket & Multi-threading"
date:   2025-12-20 08:00:00 +0700
---

Ở bài trước, chúng ta đã biết TCP là giao thức tin cậy (reliable). Hôm nay, chúng ta sẽ hiện thực hóa lý thuyết đó bằng Java. Mục tiêu của chúng ta là xây dựng một **Chat Server** có thể phục vụ hàng trăm người chat cùng lúc, chứ không chỉ là mô hình 1-1 đơn điệu.

### **1. Java Socket hoạt động như thế nào?**

Trong Java, gói `java.net` cung cấp hai class chính:
*   `ServerSocket`: Dùng cho phía Server. Nó sẽ "bind" (gắn) vào một cổng và liên tục lắng nghe.
*   `Socket`: Dùng cho cả Client và Server để trao đổi dữ liệu sau khi kết nối đã thiết lập.

Quy trình:
1.  **Server**: `serverSocket.accept()` (Chặn chương trình tại đây cho đến khi có ai đó gõ cửa).
2.  **Client**: `new Socket("ip", port)` (Gõ cửa Server).
3.  **Kết nối thành công**: Cả hai bên đều giữ một đối tượng `Socket`. Từ đối tượng này, ta lấy ra 2 luồng:
    *   `InputStream`: Để đọc dữ liệu người kia gửi đến.
    *   `OutputStream`: Để gửi dữ liệu đi.

---

### **2. Vấn đề của Server đơn luồng (Single-threaded)**

Nếu bạn viết code theo cách tuần tự thông thường:
```java
while(true) {
    Socket client = server.accept();
    xuLyClient(client); // Nếu hàm này chạy mất 10 phút, thì người thứ 2 phải chờ 10 phút mới kết nối được!
}
```
Đây là lý do tại sao các Server thực tế luôn dùng **Multi-threading** (Đa luồng). Mỗi khi có khách mới đến, chủ quán (Main Thread) sẽ thuê một nhân viên riêng (Worker Thread) để phục vụ vị khách đó, còn mình thì quay lại cửa để đón khách tiếp theo.

---

### **3. Thực hành: Xây dựng Chat Server Đa luồng**

Chúng ta sẽ tạo 2 file: `ChatServer.java` và `ChatClient.java`.

#### **File 1: ChatServer.java**

```java
import java.io.*;
import java.net.*;
import java.util.*;

public class ChatServer {
    // Cổng dịch vụ
    private static final int PORT = 12345;
    
    // Danh sách các Client đang kết nối để broadcast tin nhắn
    private static Set<PrintWriter> clientWriters = new HashSet<>();

    public static void main(String[] args) {
        System.out.println("Chat Server đang khởi động...");
        try (ServerSocket serverSocket = new ServerSocket(PORT)) {
            while (true) {
                // 1. Chờ kết nối
                Socket clientSocket = serverSocket.accept();
                System.out.println("Có người mới tham gia: " + clientSocket);
                
                // 2. Tạo luồng riêng cho khách này
                new ClientHandler(clientSocket).start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // Class xử lý riêng cho từng client (Worker Thread)
    private static class ClientHandler extends Thread {
        private Socket socket;
        private PrintWriter out;
        private BufferedReader in;

        public ClientHandler(Socket socket) {
            this.socket = socket;
        }

        public void run() {
            try {
                // Tạo luồng vào/ra
                in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                out = new PrintWriter(socket.getOutputStream(), true);

                // Thêm client này vào danh sách quản lý
                synchronized (clientWriters) {
                    clientWriters.add(out);
                }

                String message;
                // Vòng lặp đọc tin nhắn liên tục
                while ((message = in.readLine()) != null) {
                    System.out.println("Nhận được: " + message);
                    broadcast(message); // Gửi cho tất cả mọi người
                }
            } catch (IOException e) {
                System.out.println("Client đã ngắt kết nối.");
            } finally {
                // Dọn dẹp khi khách rời đi
                if (out != null) {
                    synchronized (clientWriters) {
                        clientWriters.remove(out);
                    }
                }
                try { socket.close(); } catch (IOException e) {}
            }
        }
    }

    // Hàm gửi tin nhắn cho TẤT CẢ client
    private static void broadcast(String message) {
        synchronized (clientWriters) {
            for (PrintWriter writer : clientWriters) {
                writer.println(message);
            }
        }
    }
}
```

#### **File 2: ChatClient.java**

Để test, bạn có thể chạy file này nhiều lần (mỗi lần là một cửa sổ chat khác nhau).

```java
import java.io.*;
import java.net.*;
import java.util.Scanner;

public class ChatClient {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost", 12345);
            System.out.println("Đã kết nối tới Server Chat!");

            // Luồng đọc tin nhắn từ Server (Chạy ngầm)
            new Thread(() -> {
                try {
                    BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                    String svMsg;
                    while ((svMsg = in.readLine()) != null) {
                        System.out.println(">> " + svMsg);
                    }
                } catch (IOException e) {
                    System.out.println("Mất kết nối Server!");
                }
            }).start();

            // Luồng gửi tin nhắn (Main thread)
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            Scanner scanner = new Scanner(System.in);
            while (true) {
                String input = scanner.nextLine();
                out.println(input);
            }

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

### **4. Lưu ý quan trọng khi lập trình Socket**

1.  **Đóng resources (Resource Closing):** Luôn nhớ đóng Socket, InputStream, OutputStream trong khối `finally` hoặc dùng `try-with-resources`. Nếu không, Server của bạn sẽ bị rò rỉ bộ nhớ (memory leak) và sập sau vài ngày.
2.  **Thread Safety:** Khi nhiều luồng cùng truy cập vào biến `clientWriters`, ta phải dùng `synchronized` để tránh xung đột dữ liệu (Race Condition).
3.  **Port:** Đừng dùng các port dưới 1024 (như 80, 443) vì thường cần quyền Admin. Hãy dùng các số lớn như 12345, 8080...

### **5. Bài tập về nhà**
Code hiện tại chỉ broadcast tin nhắn cho tất cả. Bạn hãy nâng cấp nó:
*   Yêu cầu người dùng nhập tên khi mới vào (Ví dụ: "Enter your name: Kiet").
*   Khi chat, hiện tên người gửi trước tin nhắn (Ví dụ: `Kiet: Hello mọi người`).
*   Thêm chức năng chat thầm (private message): `/w Son hom nay di an khong?`.

Hẹn gặp lại ở **Bài 3**, chúng ta sẽ khám phá UDP - giao thức "tốc độ bàn thờ" dùng trong Game Online!