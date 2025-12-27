---
title: "Hiểu về Đa luồng (Multithreading) trong Java qua ví dụ thực tế"
date: 2025-12-27
draft: false
categories: ["Java", "Core"]
summary: "Tại sao cần đa luồng? Hướng dẫn tạo và chạy song song 2 luồng công việc khác nhau."
---

Đa luồng (Multithreading) cho phép chương trình thực hiện nhiều công việc cùng một lúc thay vì phải chờ công việc này xong mới đến công việc khác.

Ví dụ: Khi bạn mở Word, bạn vừa có thể gõ văn bản, vừa có thể để máy tự động kiểm tra chính tả. Đó là nhờ đa luồng.

### 1. Code Demo: Cuộc đua giữa 2 luồng
Trong ví dụ này, chúng ta sẽ tạo ra 2 "công nhân" (Thread) và cho họ chạy đua đếm số từ 1 đến 5 cùng lúc.

```java
// Cách đơn giản nhất để tạo luồng: Kế thừa lớp Thread
class MyThread extends Thread {
    public void run() {
        // Đây là công việc mà luồng sẽ thực hiện
        for(int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " đang đếm: " + i);
            try {
                // Ngủ 500ms (0.5 giây) giả lập công việc nặng
                Thread.sleep(500); 
            } catch(Exception e){
                System.out.println(e);
            }
        }
    }
}

public class TestThread {
    public static void main(String args[]) {
        // Tạo 2 luồng mới
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        
        // Đặt tên cho dễ phân biệt
        t1.setName("Luồng A");
        t2.setName("Luồng B");
        
        // Kích hoạt luồng (Bắt đầu chạy hàm run)
        System.out.println("--- Bắt đầu cuộc đua ---");
        t1.start();
        t2.start();
    }
}
```

### 2. Kết quả chạy
Khi chạy chương trình, bạn sẽ thấy kết quả in ra **xen kẽ nhau** chứ không theo thứ tự tuần tự. Điều này chứng tỏ 2 luồng đang chạy song song.

```text
--- Bắt đầu cuộc đua ---
Luồng A đang đếm: 1
Luồng B đang đếm: 1
Luồng A đang đếm: 2
Luồng B đang đếm: 2
Luồng B đang đếm: 3
Luồng A đang đếm: 3
...
```

### 3. Tại sao cần `start()` mà không gọi `run()`?
* Nếu bạn gọi `t1.run()`: Máy sẽ chạy hết t1 rồi mới đến t2 (Tuần tự - Không phải đa luồng).
* Khi gọi `t1.start()`: Máy sẽ tách ra một luồng xử lý riêng biệt và chạy xong song với chương trình chính.