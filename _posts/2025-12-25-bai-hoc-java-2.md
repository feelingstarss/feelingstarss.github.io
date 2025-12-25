---
layout: post
title: "Bài 2: Xây dựng kết nối tin cậy với Socket TCP trong Java"
---
TCP là giao thức hướng kết nối, đảm bảo dữ liệu được truyền đi chính xác 100% và đúng thứ tự.
### **1. Tại sao chọn TCP?**
TCP thực hiện cơ chế bắt tay 3 bước để đảm bảo đường truyền ổn định trước khi gửi dữ liệu.

### **2. Ví dụ Code Server TCP**
```java
import java.io.*;
import java.net.*;

public class MyServer {
    public static void main(String[] args) throws IOException {
        ServerSocket server = new ServerSocket(8888);
        System.out.println("Server đang chờ kết nối...");
        
        Socket socket = server.accept();
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
        out.println("Kết nối TCP thành công!");
        
        socket.close();
        server.close();
    }
}

### **3. Ứng dụng**
Dùng trong truyền tải file, email hoặc bất kỳ ứng dụng nào không cho phép mất dữ liệu.