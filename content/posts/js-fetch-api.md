---
title: "Làm việc với API: Hướng dẫn sử dụng Fetch trong JavaScript"
date: 2025-12-27
draft: false
categories: ["JavaScript", "Web"]
summary: "Cách lấy dữ liệu JSON từ server bên ngoài (API) mà không cần tải lại trang."
---

Ngày xưa để lấy dữ liệu từ Server, chúng ta dùng `XMLHttpRequest` rất dài dòng. Bây giờ, JavaScript cung cấp **Fetch API** cực kỳ mạnh mẽ và dễ dùng.

Trong ví dụ này, mình sẽ lấy một "Công việc mẫu" từ trang API miễn phí `jsonplaceholder` và hiển thị lên màn hình.

### 1. Code Demo
Bạn copy đoạn này chạy thử. Bấm nút và quan sát kết quả hiện ra ngay lập tức mà web không hề bị nháy (reload).

```html
<!DOCTYPE html>
<html>
<body>

    <h2>Demo Fetch API</h2>
    <button onclick="getData()">Lấy dữ liệu từ Server</button>
    
    <div id="result" style="margin-top: 20px; padding: 10px; border: 1px solid #ccc; display: none;">
        </div>

    <script>
        // Sử dụng async/await để code trông gọn hơn
        async function getData() {
            const displayDiv = document.getElementById("result");
            displayDiv.style.display = "block";
            displayDiv.innerHTML = "Đang tải...";
            
            try {
                // 1. Gửi yêu cầu đến API
                const response = await fetch('[https://jsonplaceholder.typicode.com/todos/1](https://jsonplaceholder.typicode.com/todos/1)');
                
                // 2. Chuyển đổi dữ liệu nhận được sang JSON
                const data = await response.json();
                
                // 3. Hiển thị ra màn hình
                displayDiv.innerHTML = 
                    "<strong>Title:</strong> " + data.title + "<br>" +
                    "<strong>Status:</strong> " + (data.completed ? "Hoàn thành" : "Chưa xong");
                    
            } catch (error) {
                console.log("Lỗi rồi: " + error);
            }
        }
    </script>

</body>
</html>
```

### 2. Giải thích `async` và `await`
* **`fetch`**: Là hành động tốn thời gian (phải chờ Server trả lời).
* **`await`**: Bảo JavaScript là "Hãy tạm dừng ở dòng này, chờ fetch xong rồi mới chạy tiếp dòng dưới".
* Nhờ vậy, code đọc từ trên xuống dưới rất dễ hiểu, không bị lồng vào nhau như Callback cũ.