---
title: "Kiểm tra dữ liệu Form (Validation) bằng JavaScript"
date: 2025-12-27
draft: false
categories: ["JavaScript", "Web"]
summary: "Cách chặn người dùng gửi form rỗng hoặc nhập mật khẩu quá ngắn."
---

Form Validation là kỹ thuật bắt buộc phải có để đảm bảo dữ liệu gửi lên Server là sạch và đúng định dạng. Dưới đây là ví dụ kiểm tra form Đăng Ký.

### 1. Yêu cầu
* Tên đăng nhập không được để trống.
* Mật khẩu phải dài hơn 6 ký tự.

### 2. Code Demo

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .error { color: red; font-style: italic; }
    </style>
</head>
<body>

<h2>Form Đăng Ký</h2>

<form name="regForm" onsubmit="return validateForm()" method="post">
  Tên đăng nhập: <input type="text" name="username"><br><br>
  
  Mật khẩu: <input type="password" name="password"><br><br>
  
  <input type="submit" value="Đăng Ký">
</form>

<script>
function validateForm() {
  // 1. Lấy giá trị từ form
  let user = document.forms["regForm"]["username"].value;
  let pass = document.forms["regForm"]["password"].value;
  
  // 2. Kiểm tra tên rỗng
  if (user == "") {
    alert("Lỗi: Tên đăng nhập không được để trống!");
    return false; // Chặn không cho gửi form
  }
  
  // 3. Kiểm tra mật khẩu ngắn
  if (pass.length < 6) {
    alert("Lỗi: Mật khẩu phải dài hơn 6 ký tự!");
    return false;
  }
  
  // Nếu mọi thứ ok
  alert("Dữ liệu hợp lệ! Đang gửi đi...");
  return true; 
}
</script>

</body>
</html>
```

### 3. Phân tích
* Sự kiện `onsubmit="return validateForm()"`: Đây là chốt chặn quan trọng nhất.
* `return false`: Báo cho trình duyệt biết là "Có lỗi rồi, đừng tải lại trang, đừng gửi dữ liệu đi".
* `document.forms`: Cách truy xuất nhanh đến các thẻ input trong form.