---
title: "Tạo đồng hồ kỹ thuật số Realtime với JS"
date: 2025-12-27
draft: false
categories: ["JavaScript", "Web"]
summary: "Sử dụng đối tượng Date và hàm setTimeout để cập nhật thời gian liên tục trên màn hình."
---

Làm thế nào để hiển thị giờ hiện tại và khiến nó tự nhảy số mỗi giây? Chúng ta sẽ sử dụng hàm `setTimeout` (hoặc `setInterval`) để làm việc này.

### 1. Code Demo
Copy đoạn code sau vào file HTML để chạy thử.

```html
<!DOCTYPE html>
<html>
<body onload="startTime()">

    <h2>Đồng hồ bây giờ là:</h2>
    
    <div id="clockDisplay" style="font-size: 40px; font-weight: bold; color: #0779e4;"></div>

    <script>
        function startTime() {
            // 1. Lấy thời gian hiện tại
            const today = new Date();
            let h = today.getHours();
            let m = today.getMinutes();
            let s = today.getSeconds();
            
            // 2. Thêm số 0 vào trước nếu nhỏ hơn 10 (Ví dụ: 9:5 -> 09:05)
            m = checkTime(m);
            s = checkTime(s);
            
            // 3. Hiển thị lên màn hình
            document.getElementById('clockDisplay').innerHTML =  h + ":" + m + ":" + s;
            
            // 4. Gọi lại hàm này sau 1000ms (1 giây)
            setTimeout(startTime, 1000);
        }

        // Hàm phụ trợ để thêm số 0
        function checkTime(i) {
            if (i < 10) {i = "0" + i};  
            return i;
        }
    </script>

</body>
</html>
```

### 2. Giải thích logic
1.  **`new Date()`**: Lấy thời gian thực từ máy tính của người dùng.
2.  **Logic thêm số 0**: Máy tính trả về số `5`, nhưng đồng hồ chuẩn phải là `05`. Hàm `checkTime` giải quyết việc này.
3.  **`setTimeout(startTime, 1000)`**: Đây là chìa khóa. Sau khi hiển thị giờ xong, nó hẹn giờ "1 giây sau hãy chạy lại tôi". Việc này tạo thành một vòng lặp vô tận, giúp đồng hồ chạy mãi mãi.