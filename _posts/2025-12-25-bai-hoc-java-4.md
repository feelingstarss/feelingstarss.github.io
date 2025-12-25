### 4. Bài 4: JavaScript & Lập trình bất đồng bộ
**File:** `2025-12-04-javascript-async.md`
```markdown
---
layout: post
title: "Bài 4: JavaScript và sức mạnh của lập trình bất đồng bộ"
---
Lập trình mạng đòi hỏi thời gian chờ phản hồi, JavaScript xử lý việc này cực tốt bằng Async/Await.
### 1. Vấn đề của lập trình đồng bộ
Trong mạng, nếu bạn chờ phản hồi mà dừng toàn bộ chương trình, ứng dụng sẽ bị "đơ" (lag).

### 2. Giải pháp Async/Await
```javascript
async function getData() {
    try {
        let response = await fetch('[https://api.example.com/data](https://api.example.com/data)');
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("Lỗi rồi:", error);
    }
}