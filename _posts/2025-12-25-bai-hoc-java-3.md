---
layout: post
title: "Bài 3: Tối ưu tốc độ truyền tải với giao thức UDP"
---
UDP nhanh hơn TCP nhưng không đảm bảo độ tin cậy. Vậy khi nào chúng ta nên dùng nó?
### 1. Đặc điểm của UDP
UDP là giao thức không hướng kết nối (Connectionless). Nó gửi các gói tin đi mà không cần chờ xác nhận từ phía nhận.

### 2. Ví dụ Code gửi dữ liệu
```java
DatagramSocket socket = new DatagramSocket();
byte[] buffer = "Xin chào UDP".getBytes();
InetAddress address = InetAddress.getByName("localhost");
DatagramPacket packet = new DatagramPacket(buffer, buffer.length, address, 9000);
socket.send(packet);