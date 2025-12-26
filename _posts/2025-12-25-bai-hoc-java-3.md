---
layout: post
title:  "Bài 3: UDP - Giao thức \"Bắn và Quên\" dành cho Game & Livestream"
---

Nếu TCP là một anh bưu tá cẩn thận, bắt bạn ký nhận từng lá thư, thì UDP (User Datagram Protocol) giống như một cái máy bắn bóng tennis: nó cứ bắn liên tục về phía bạn, việc bạn đỡ được hay không nó không quan tâm. Nghe có vẻ vô trách nhiệm? Nhưng chính sự "vô tâm" đó lại là chìa khóa cho tốc độ (performance).

### **1. Tại sao Game Liên Minh/PUBG dùng UDP?**

Hãy tưởng tượng bạn đang chơi game bắn súng.
*   **Trường hợp dùng TCP:** Bạn bắn 1 viên đạn. Gói tin bị lag 0.5s. Server dừng cả trận đấu lại để chờ gói tin đó đến nơi rồi mới cho chạy tiếp. -> **LAG GIẬT CỤC.**
*   **Trường hợp dùng UDP:** Gói tin viên đạn bị mất? Kệ nó. Server cập nhật luôn vị trí mới của nhân vật. Trên màn hình bạn có thể thấy nhân vật hơi "dịch chuyển tức thời" một chút, nhưng trò chơi vẫn mượt mà. -> **TRẢI NGHIỆM TỐT HƠN.**

UDP phù hợp khi: **Tốc độ > Sự chính xác tuyệt đối.**

---

### **2. Code Demo Java: Gửi tin nhắn Broadcast**

Khác với TCP (cần `Socket` và `ServerSocket`), UDP sử dụng:
*   `DatagramSocket`: Để gửi/nhận.
*   `DatagramPacket`: Là cái "gói" chứa dữ liệu và địa chỉ người nhận.

Chúng ta sẽ viết 2 chương trình: **Người Gửi (Sender)** và **Người Nhận (Receiver)**.

#### File 1: UDPReceiver.java (Chạy cái này trước để chờ tin)

```java
import java.net.*;

public class UDPReceiver {
    public static void main(String[] args) throws Exception {
        // 1. Mở cổng 9876 để lắng nghe
        DatagramSocket socket = new DatagramSocket(9876);
        byte[] buffer = new byte[1024]; // Tạo mảng byte để chứa dữ liệu nhận được

        System.out.println("Đang chờ tin nhắn UDP...");

        while (true) {
            // 2. Tạo gói tin rỗng để hứng dữ liệu
            DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
            
            // 3. Nhận dữ liệu (Code sẽ dừng ở đây cho đến khi có tin đến)
            socket.receive(packet);
            
            // 4. Xử lý dữ liệu
            String msg = new String(packet.getData(), 0, packet.getLength());
            System.out.println("Nhận được từ " + packet.getAddress() + ": " + msg);
        }
    }
}
```

#### File 2: UDPSender.java

```java
import java.net.*;
import java.util.Scanner;

public class UDPSender {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket(); // Không cần specify port cho người gửi
        InetAddress ip = InetAddress.getByName("localhost");
        Scanner scanner = new Scanner(System.in);

        System.out.println("Nhập tin nhắn để bắn đi:");
        while(true) {
            String input = scanner.nextLine();
            byte[] data = input.getBytes();

            // Đóng gói tin: (Dữ liệu, Độ dài, IP người nhận, Port người nhận)
            DatagramPacket packet = new DatagramPacket(data, data.length, ip, 9876);
            
            socket.send(packet);
            System.out.println("Đã bắn tin đi!");
        }
    }
}
```

---

### **3. Sự khác biệt trong Code (So với TCP)**
1.  **Không có `accept()`:** UDP không cần thiết lập kết nối (connection-less). Nó cứ thế mà lắng nghe thôi.
2.  **Giới hạn kích thước:** Một gói tin UDP (`DatagramPacket`) thường bị giới hạn kích thước (thường là 64KB). Nếu bạn gửi file lớn, bạn phải tự cắt nhỏ nó ra. TCP làm việc này tự động giúp bạn (stream).
3.  **Thứ tự không đảm bảo:** Bạn gửi tin A trước, tin B sau. Nhưng người nhận có thể nhận B trước, A sau. Nếu muốn đúng thứ tự, bạn phải tự đánh số trong code (Ví dụ: `1:Hello`, `2:How are you`).

### **4. Bài tập nâng cao**
Hãy thử viết một ứng dụng **Stream Audio đơn giản**:
*   Sender: Đọc một file nhạc `.wav`, cắt thành từng mảng byte nhỏ (chunk) 1024 bytes.
*   Gửi liên tục qua UDP.
*   Receiver: Nhận được chunk nào thì phát (play) luôn chunk đó.
-> Đó chính là nguyên lý sơ khai của Spotify hay Youtube đấy!

Hẹn gặp lại ở **Bài 4**, chúng ta sẽ tạm biệt Java một chút để qua một ngôn ngữ "thống trị" Web: **JavaScript** và cơ chế Bất đồng bộ (Async) của nó.