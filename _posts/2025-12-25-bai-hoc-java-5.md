---
layout: post
title:  "Bài 5: Fetch API & JSON - Cây cầu nối Frontend và Backend"
---

Ngày nay, Frontend (React/Vue/Angular) và Backend (Java/Node.js) thường là hai dự án tách biệt. Chúng "nói chuyện" với nhau thông qua **API (Application Programming Interface)** trả về dữ liệu định dạng **JSON**.

Trong quá khứ, chúng ta dùng `XMLHttpRequest` (AJAX) rất cực khổ. Giờ đây, **Fetch API** đã được tích hợp sẵn vào mọi trình duyệt hiện đại.

### 1. JSON là gì? (JavaScript Object Notation)
Nó là định dạng dữ liệu dạng text, nhẹ và dễ đọc.
```json
{
  "name": "Kiet Nguyen",
  "skills": ["Java", "JavaScript"],
  "is_admin": true
}
```
*   **Backend gửi đi:** Java Object -> Biến thành chuỗi JSON (Serialization).
*   **Frontend nhận về:** Chuỗi JSON -> Biến thành JavaScript Object (Deserialization).

### 2. Các phương thức HTTP cơ bản (HTTP Verbs)
Khi gọi API, bạn phải nói rõ bạn muốn làm gì:
*   **GET**: Lấy dữ liệu về (Mặc định).
*   **POST**: Thêm mới dữ liệu.
*   **PUT**: Cập nhật dữ liệu (ghi đè).
*   **DELETE**: Xóa dữ liệu.

### 3. Code chuẩn: Viết API Wrapper tái sử dụng

Đừng bao giờ gọi `fetch` trần trụi ở khắp mọi nơi trong code của bạn. Hãy viết một hàm chung (Helper function) để tái sử dụng và xử lý lỗi tập trung.

```javascript
const API_URL = "https://reqres.in/api"; // URL API Demo miễn phí

/**
 * Hàm chung để gọi API
 * @param {string} endpoint - Đường dẫn (ví dụ: '/users')
 * @param {string} method - GET, POST...
 * @param {object} body - Dữ liệu gửi đi (nếu có)
 */
async function callAPI(endpoint, method = 'GET', body = null) {
    const options = {
        method: method,
        headers: {
            'Content-Type': 'application/json',
            // Nếu API cần đăng nhập, truyền token vào đây
            // 'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
    };

    if (body) {
        options.body = JSON.stringify(body); // Chuyển Object thành JSON string
    }

    try {
        const response = await fetch(API_URL + endpoint, options);

        // Kiểm tra nếu Server trả về lỗi (404, 500...)
        if (!response.ok) {
            throw new Error(`Lỗi API: ${response.status}`);
        }

        const data = await response.json();
        return data;

    } catch (error) {
        console.error("Gọi API thất bại:", error);
        throw error; // Ném lỗi ra để bên ngoài xử lý tiếp
    }
}
```

### 4. Cách sử dụng (Clean Code)

Giờ đây code của bạn sẽ cực kỳ gọn gàng:

**Ví dụ 1: Lấy danh sách User (GET)**
```javascript
async function getListUsers() {
    try {
        const data = await callAPI('/users?page=2');
        console.log("Danh sách User:", data.data);
    } catch (e) {
        alert("Không tải được danh sách!");
    }
}
```

**Ví dụ 2: Tạo User mới (POST)**
```javascript
async function createUser() {
    const newUser = {
        name: "FeelingStarts",
        job: "Fullstack Dev"
    };

    try {
        const result = await callAPI('/users', 'POST', newUser);
        console.log("Tạo thành công, ID mới:", result.id);
        alert("Thêm thành công!");
    } catch (e) {
        alert("Thêm thất bại!");
    }
}
```

### 5. Lưu ý về CORS (Cross-Origin Resource Sharing)
Một ngày đẹp trời, bạn thấy lỗi đỏ lòm trên Console: `Access to fetch... has been blocked by CORS policy`.
Đừng hoảng! Đây là cơ chế bảo mật của trình duyệt. Nó chặn không cho Web A gọi API của Web B nếu Web B không cho phép.
*   **Cách đơn giản:** Cài Extension "Allow CORS" (chỉ dùng khi dev).
*   **Cách đúng:** Nhờ Backend Developer cấu hình cho phép domain của bạn truy cập (trong Server Java/Nodejs).

Hẹn gặp lại ở **Bài 6**, chúng ta sẽ làm một thứ ngầu hơn nhiều: **Chat Real-time** trên nền Web với WebSocket!