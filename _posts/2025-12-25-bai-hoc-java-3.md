---
layout: post
title: "Bài 3: Tối ưu tốc độ truyền tải với giao thức UDP"
---
UDP ưu tiên tốc độ hơn sự tin cậy, cực kỳ phù hợp cho các ứng dụng thời gian thực.
### **1. Bản chất của UDP**
UDP gửi các gói tin đi mà không cần xác nhận, giúp giảm thiểu độ trễ tối đa.

### **2. Ví dụ Code gửi gói tin UDP**
```java
import java.net.*;

public class UdpSender {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket();
        byte[] data = "Hello UDP".getBytes();
        
        InetAddress ip = InetAddress.getByName("localhost");
        DatagramPacket packet = new DatagramPacket(data, data.length, ip, 9000);
        
        socket.send(packet);
        socket.close();
    }
}

### **3. Ứng dụng thực tế**
Livestream video, Game online (Ping thấp), và các dịch vụ Voice chat.