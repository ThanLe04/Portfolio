---
title: "Xây dựng ứng dụng Chat đơn giản với Java Socket (TCP)"
date: 2025-12-27
draft: false
categories: ["Java", "Lập trình mạng"]
summary: "Hướng dẫn tạo kết nối TCP đơn giản giữa Client và Server để trao đổi tin nhắn."
---

Lập trình mạng là một phần quan trọng trong Java. Hôm nay mình sẽ chia sẻ code demo tạo một ứng dụng Chat đơn giản sử dụng `java.net.Socket`.

### 1. Server (Máy chủ)
Server sẽ mở cổng 5000 và chờ Client kết nối.

```java
import java.io.*;
import java.net.*;

public class SimpleServer {
    public static void main(String[] args) {
        try {
            ServerSocket serverSocket = new ServerSocket(5000);
            System.out.println("Server đang chạy tại port 5000...");
            
            Socket socket = serverSocket.accept(); // Chờ kết nối
            System.out.println("Client đã kết nối!");
            
            // Luồng đọc dữ liệu từ Client
            DataInputStream dis = new DataInputStream(socket.getInputStream());
            String message = dis.readUTF();
            System.out.println("Client nói: " + message);
            
            serverSocket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 2. Client (Máy khách)
Client kết nối đến localhost cổng 5000 và gửi tin nhắn.

```java
import java.io.*;
import java.net.*;

public class SimpleClient {
    public static void main(String[] args) {
        try {
            Socket socket = new Socket("localhost", 5000);
            
            // Gửi tin nhắn đi
            DataOutputStream dos = new DataOutputStream(socket.getOutputStream());
            dos.writeUTF("Chào Server, mình là Client đây!");
            
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 3. Kết quả
Khi chạy chương trình, Server sẽ lắng nghe và nhận được dòng tin nhắn từ Client gửi tới. Đây là nền tảng cơ bản nhất của mọi ứng dụng chat mạng LAN.