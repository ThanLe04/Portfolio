---
title: "Giao thức UDP trong Java: Gửi nhận dữ liệu không kết nối"
date: 2025-12-27
draft: false
categories: ["Java", "Lập trình mạng"]
summary: "Tìm hiểu cách sử dụng DatagramSocket để gửi dữ liệu nhanh qua giao thức UDP."
---

Khác với TCP (ở bài trước), **UDP** là giao thức không hướng kết nối (connectionless). Nó cho phép gửi dữ liệu đi cực nhanh mà không cần thiết lập đường truyền trước, nhưng không đảm bảo dữ liệu đến nơi 100%.

Dưới đây là ví dụ kinh điển: Một chương trình gửi tin nhắn từ Sender sang Receiver.

### 1. Code bên Gửi (Sender)
Sender sẽ đóng gói dữ liệu vào `DatagramPacket` và bắn sang phía Receiver.

```java
import java.net.*;

public class UDPSender {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket();
        
        String str = "Xin chào UDP Receiver, đây là tin nhắn gửi qua mạng!";
        InetAddress ip = InetAddress.getByName("localhost");
        
        // Đóng gói dữ liệu (Data + Độ dài + Địa chỉ IP + Cổng đích)
        DatagramPacket packet = new DatagramPacket(str.getBytes(), str.length(), ip, 9876);
        
        // Gửi đi
        socket.send(packet);
        System.out.println("Đã gửi gói tin đi!");
        
        socket.close();
    }
}
```

### 2. Code bên Nhận (Receiver)
Receiver phải mở đúng cổng (ở đây là 9876) để hứng gói tin.

```java
import java.net.*;

public class UDPReceiver {
    public static void main(String[] args) throws Exception {
        // Mở cổng 9876 để lắng nghe
        DatagramSocket socket = new DatagramSocket(9876);
        byte[] buffer = new byte[1024]; // Tạo vùng đệm để chứa dữ liệu
        
        DatagramPacket packet = new DatagramPacket(buffer, 1024);
        
        System.out.println("Đang chờ dữ liệu UDP...");
        socket.receive(packet); // Chờ nhận gói tin (Code sẽ dừng tại đây đến khi có tin tới)
        
        // Chuyển đổi byte thành chuỗi String để đọc
        String str = new String(packet.getData(), 0, packet.getLength());
        System.out.println("Đã nhận được: " + str);
        
        socket.close();
    }
}
```

### 3. Lưu ý khi chạy
Với UDP, bạn **phải chạy Receiver trước** để nó mở cổng chờ sẵn. Nếu chạy Sender trước thì gói tin gửi đi sẽ bị thất lạc (vì không ai nhận) và không báo lỗi gì cả. Đây chính là đặc điểm "không đảm bảo" của UDP.