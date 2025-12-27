---
title: "Kỹ thuật Đọc và Ghi file Text trong Java IO"
date: 2025-12-27
draft: false
categories: ["Java", "Core"]
summary: "Hướng dẫn sử dụng FileWriter và FileReader để lưu trữ dữ liệu vĩnh viễn trên ổ cứng."
---

Trong lập trình, dữ liệu lưu trên RAM (biến, mảng) sẽ mất đi khi tắt chương trình. Để lưu trữ dữ liệu lâu dài (Persistent), cách đơn giản nhất là ghi ra file.

Hôm nay mình sẽ demo cách ghi một chuỗi văn bản vào file `data.txt` và đọc lại nó lên màn hình.

### 1. Ghi file (Write File)
Chúng ta sử dụng lớp `FileWriter`. Lưu ý là thao tác file luôn cần bỏ vào khối `try-catch` để bắt lỗi (ví dụ lỗi đầy ổ cứng, không có quyền ghi...).

```java
import java.io.FileWriter;
import java.io.IOException;

public class WriteFileExample {
    public static void main(String args[]) {
        try {
            // Tạo đối tượng FileWriter, trỏ đến file data.txt
            FileWriter fw = new FileWriter("data.txt");
            
            // Nội dung cần ghi
            String content = "Xin chào, đây là dữ liệu được lưu từ Java!";
            
            // Thực hiện ghi
            fw.write(content);
            
            // Quan trọng: Phải đóng file sau khi ghi xong
            fw.close();
            
            System.out.println("Đã ghi file thành công!");
        } catch (IOException e) {
            System.out.println("Có lỗi xảy ra: " + e);
        }
    }
}
```

### 2. Đọc file (Read File)
Để đọc file, chúng ta dùng `FileReader`. Nó sẽ đọc từng ký tự (character) dưới dạng mã ASCII, nên ta cần ép kiểu về `(char)` để xem được.

```java
import java.io.FileReader;

public class ReadFileExample {
    public static void main(String args[]) {
        try {
            FileReader fr = new FileReader("data.txt");
            
            int i;
            // Đọc từng ký tự cho đến khi hết file (kết quả trả về -1)
            while ((i = fr.read()) != -1) {
                System.out.print((char) i);
            }
            
            fr.close();
        } catch (Exception e) {
            System.out.println("Không tìm thấy file hoặc lỗi đọc file.");
        }
    }
}
```

### 3. Kết luận
* **FileWriter**: Dùng để xuất dữ liệu ra.
* **FileReader**: Dùng để lấy dữ liệu vào.
* Luôn nhớ `close()` file để tránh rò rỉ bộ nhớ.