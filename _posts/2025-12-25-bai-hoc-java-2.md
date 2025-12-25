---
layout: post
title: "Bài 2: Xây dựng kết nối tin cậy với Socket TCP trong Java"
---
Tìm hiểu cách sử dụng bộ đôi ServerSocket và Socket để truyền tải dữ liệu chính xác tuyệt đối.
### 1. Tại sao dùng TCP?
TCP (Transmission Control Protocol) đảm bảo dữ liệu gửi đi không bị mất mát và đúng thứ tự.

### 2. Ví dụ Code minh họa (Server)
```java
import java.io.*;
import java.net.*;

public class SimpleServer {
    public static void main(String[] args) throws IOException {
        ServerSocket server = new ServerSocket(8080);
        System.out.println("Server đang chờ...");
        Socket socket = server.accept();
        System.out.println("Client đã kết nối!");
    }
}