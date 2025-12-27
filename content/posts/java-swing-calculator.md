---
title: "Lập trình giao diện Java Swing: Máy tính bỏ túi đơn giản"
date: 2025-12-27
draft: false
categories: ["Java", "Swing"]
summary: "Hướng dẫn tạo cửa sổ ứng dụng (GUI) với JFrame và xử lý sự kiện nút bấm trong Java."
---

Java Swing là bộ thư viện mạnh mẽ để tạo giao diện người dùng (GUI) trên máy tính. Trong bài này, mình sẽ hướng dẫn các bạn tạo một ứng dụng "Máy tính bỏ túi" siêu đơn giản: Nhập 2 số và bấm nút để tính tổng.

### 1. Thiết kế giao diện
Chúng ta sẽ sử dụng các thành phần cơ bản sau của Swing:
* `JFrame`: Khung cửa sổ chính của ứng dụng.
* `JTextField`: Ô để người dùng nhập số.
* `JButton`: Nút bấm để thực hiện phép tính.
* `JLabel`: Dùng để hiện thị các dòng chữ hướng dẫn.



### 2. Code hoàn chỉnh
Các bạn có thể copy đoạn code sau và chạy thử trong NetBeans hoặc IntelliJ IDEA.

```java
import javax.swing.*;
import java.awt.event.*;

public class SimpleCalculator {
    public static void main(String[] args) {
        // 1. Tạo khung cửa sổ (Frame)
        JFrame f = new JFrame("Máy tính Java Swing");
        
        // 2. Tạo các ô nhập liệu (Text Field)
        final JTextField tf1 = new JTextField();
        tf1.setBounds(50, 50, 150, 20); // Vị trí x, y và kích thước
        
        final JTextField tf2 = new JTextField();
        tf2.setBounds(50, 100, 150, 20);
        
        final JTextField tf3 = new JTextField();
        tf3.setBounds(50, 150, 150, 20);
        tf3.setEditable(false); // Ô kết quả không cho nhập, chỉ hiển thị
        
        // 3. Tạo nút bấm (Button)
        JButton b_cong = new JButton("+");
        b_cong.setBounds(50, 200, 50, 50);
        
        JButton b_tru = new JButton("-");
        b_tru.setBounds(120, 200, 50, 50);

        // 4. Xử lý sự kiện khi bấm nút Cộng
        b_cong.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String s1 = tf1.getText();
                String s2 = tf2.getText();
                int a = Integer.parseInt(s1);
                int b = Integer.parseInt(s2);
                int c = a + b; // Tính tổng
                tf3.setText(String.valueOf(c)); // Hiện kết quả
            }
        });
        
        // Xử lý sự kiện khi bấm nút Trừ
        b_tru.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String s1 = tf1.getText();
                String s2 = tf2.getText();
                int a = Integer.parseInt(s1);
                int b = Integer.parseInt(s2);
                int c = a - b;
                tf3.setText(String.valueOf(c));
            }
        });

        // 5. Thêm tất cả vào cửa sổ và hiển thị
        f.add(tf1); f.add(tf2); f.add(tf3);
        f.add(b_cong); f.add(b_tru);
        
        f.setSize(300, 300);
        f.setLayout(null);
        f.setVisible(true);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}
```

### 3. Giải thích code
* Hàm `setBounds(x, y, width, height)`: Dùng để căn chỉnh vị trí của nút bấm và ô nhập liệu thủ công (không dùng Layout Manager).
* Interface `ActionListener`: Dùng để "lắng nghe" hành động click chuột của người dùng. Khi nút được bấm, code trong hàm `actionPerformed` sẽ chạy.

Hy vọng bài viết này giúp bạn hiểu cơ bản về cách tạo form trong Java!