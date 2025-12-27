---
title: "Bài tập JS: Đổi màu nền ngẫu nhiên với DOM"
date: 2025-12-27
draft: false
categories: ["JavaScript", "Web"]
summary: "Sử dụng JavaScript để can thiệp vào CSS, tạo hiệu ứng đổi màu vui mắt."
---

DOM (Document Object Model) cho phép JavaScript "nói chuyện" và thay đổi các phần tử HTML/CSS trên trang web.

Trong bài này, mình sẽ viết một hàm JS đơn giản: Mỗi khi người dùng bấm nút, trang web sẽ tự động chọn một màu bất kỳ để làm hình nền.

### 1. Code HTML & JS
Bạn có thể copy đoạn này lưu thành file `.html` để chạy thử ngay trên trình duyệt.

```html
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <title>Đổi màu nền</title>
    <style>
        body {
            transition: background-color 0.5s; /* Hiệu ứng chuyển màu mượt mà */
            text-align: center;
            padding-top: 100px;
            font-family: sans-serif;
        }
        button {
            padding: 15px 30px;
            font-size: 20px;
            cursor: pointer;
            background-color: white;
            border: 2px solid #333;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <h1>Bấm nút bên dưới để đổi màu!</h1>
    
    <button onclick="changeColor()">Đổi màu ngay</button>

    <script>
        function changeColor() {
            // 1. Tạo 3 số ngẫu nhiên từ 0 đến 255 (tương ứng Red, Green, Blue)
            const r = Math.floor(Math.random() * 256);
            const g = Math.floor(Math.random() * 256);
            const b = Math.floor(Math.random() * 256);
            
            // 2. Ghép lại thành chuỗi màu RGB
            const color = `rgb(${r}, ${g}, ${b})`;
            
            // 3. Gán màu đó cho body
            document.body.style.backgroundColor = color;
            
            // In ra console để kiểm tra
            console.log("Đã đổi sang màu: " + color);
        }
    </script>

</body>
</html>
```

### 2. Giải thích
* `Math.random()`: Sinh ra số ngẫu nhiên từ 0 đến 1.
* `Math.floor()`: Làm tròn số xuống.
* `document.body.style.backgroundColor`: Đây là lệnh DOM dùng để can thiệp vào thuộc tính CSS `background-color` của thẻ `<body>`.

Đây là ví dụ đơn giản nhất để thấy sức mạnh của JS trong việc tương tác với giao diện người dùng.