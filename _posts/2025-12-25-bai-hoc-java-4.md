---
layout: post
title:  "Bài 4: Javascript Event Loop & Async Await - Vì sao không nên để người dùng chờ?"
date:   2025-12-22 08:00:00 +0700
---

Chào mừng trở lại! Chúng ta đã "vọc" đủ sâu với Java Socket (Backend). Bây giờ hãy nhảy sang phía Frontend. Khi bạn làm việc với Network trên trình duyệt (Browser), quy tắc số 1 là: **Không bao giờ được chặn (block) giao diện người dùng.**

Nếu code mạng của bạn chạy mất 5 giây để tải dữ liệu và trong 5 giây đó trỏ chuột bị đơ, không cuộn trang được -> Người dùng sẽ tắt web ngay lập tức. Đây là lúc **Lập trình bất đồng bộ (Asynchronous Programming)** lên ngôi.

### **1. Sự ảo diệu của JavaScript: Đơn luồng nhưng không cô đơn**

JavaScript là ngôn ngữ **Single-threaded** (Đơn luồng). Nghĩa là tại một thời điểm, nó schỉ làm được **một việc duy nhất**.
*   Vậy tại sao nó có thể vừa tải nhạc, vừa đếm giờ, vừa nhận sự kiện click chuột?
*   Đó là nhờ cơ chế **Event Loop**.

Hãy tưởng tượng JS là một anh phục vụ bàn duy nhất trong quán cafe:
1.  Khách A gọi Cafe (Yêu cầu mạng).
2.  JS ghi order, đưa phiếu cho pha chế (Web APIs/Browser) làm.
3.  JS quay sang phục vụ Khách B ngay lập tức (Xử lý giao diện), **không đứng chờ pha chế**.
4.  Khi Cafe xong, pha chế bấm chuông (Callback Queue).
5.  JS phục vụ xong Khách B, quay lại lấy Cafe đưa cho Khách A.

### **2. Sự tiến hóa: Từ Callback Hell đến Async/Await**

#### Thời kỳ đồ đá: Callback
Cách cũ để xử lý việc "khi nào xong thì gọi tôi":
```javascript
getData(function(a) {
    getMoreData(a, function(b) {
        getMoreMoreData(b, function(c) {
            getMoreMoreMoreData(c, function(d) {
                console.log(d);
            });
        });
    });
});
```
-> Mã nguồn nhìn như hình tam giác. Đây gọi là **Callback Hell** (Địa ngục Callback), cực khó bảo trì.

#### Thời kỳ hiện đại: Async / Await (Cú pháp của ES8)
Async/Await giúp code bất đồng bộ nhìn "y chang" code đồng bộ tuần tự. Dễ đọc, dễ hiểu.

```javascript
// Thêm từ khóa 'async' vào đầu hàm
async function xuLyCongViec() {
    try {
        console.log("1. Bắt đầu gọi API...");
        
        // Từ khóa 'await': Tạm dừng hàm này tại đây, đợi lấy xong dữ liệu mới chạy dòng tiếp theo
        // NHƯNG giao diện bên ngoài vẫn mượt, không bị đơ!
        let response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
        let data = await response.json();
        
        console.log("2. Dữ liệu đã về:", data);
        console.log("3. Tên công việc:", data.title);
        
    } catch (error) {
        // Xử lý lỗi cực gọn với try-catch truyền thống
        console.error("Ôi hỏng rồi:", error);
    }
}

xuLyCongViec();
console.log("Dòng này sẽ chạy TRƯỚC dòng 2 và 3 vì JS không chờ đợi!");
```

### **3. Quy tắc vàng khi gọi API mạng**
1.  **Luôn dùng `try...catch`**: Mạng internet không ổn định. Server có thể sập, wifi có thể rớt. Không bắt lỗi -> Ứng dụng "chết" bất đắc kỳ tử.
2.  **Hiển thị Loading**: Trước khi `await`, hãy hiện cái vòng quay loading. Sau khi xong (trong `finally`), hãy tắt nó đi.
3.  **Không `await` trong vòng lặp `forEach`**: Đây là lỗi kinh điển.
    *   Sai: `arr.forEach(async item => { await ... })` -> Nó sẽ chạy song song hết, không chờ nhau.
    *   Đúng: Dùng vòng lặp `for...of` nếu muốn chạy tuần tự.

### **4. Bài tập thực hành**
Bạn hãy mở Console của trình duyệt (F12 -> Console) và copy đoạn code sau để chạy thử:

```javascript
function doi(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function chayThu() {
    console.log("Bắt đầu đếm ngược...");
    await doi(1000); console.log("3...");
    await doi(1000); console.log("2...");
    await doi(1000); console.log("1...");
    console.log("Happy New Year!");
}

chayThu();
```

Ở **Bài 5**, chúng ta sẽ ứng dụng Async/Await này để làm việc với **Fetch API** - tiêu chuẩn mới để giao tiếp Client-Server thay thế cho AJAX cũ kỹ.