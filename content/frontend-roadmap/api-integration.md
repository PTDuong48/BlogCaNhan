---
title: "API Integration"
date: 2025-01-20
description: "Kết nối Frontend với Backend API"
weight: 10
---

# API Integration

API Integration là cách Frontend giao tiếp với Backend để lấy và gửi dữ liệu. Đây là kỹ năng quan trọng trong phát triển web hiện đại.

## 🔌 API là gì?

API (Application Programming Interface) là giao diện cho phép các ứng dụng giao tiếp với nhau. Trong web development, Frontend thường gọi REST API hoặc GraphQL API từ Backend.

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/ByGJQzlzxQg" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/APIIntegration.jpg" alt="API Integration" />

## 📚 Các phương pháp gọi API

### 1. Fetch API

```javascript
// GET request
fetch("https://api.example.com/users")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));

// POST request
fetch("https://api.example.com/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "John",
    email: "john@example.com",
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```

### 2. Axios

```javascript
import axios from "axios";

// GET request
axios
  .get("https://api.example.com/users")
  .then((response) => console.log(response.data))
  .catch((error) => console.error(error));

// POST request
axios
  .post("https://api.example.com/users", {
    name: "John",
    email: "john@example.com",
  })
  .then((response) => console.log(response.data));
```

### 3. React Query (TanStack Query)

```jsx
import { useQuery } from "@tanstack/react-query";

function Users() {
  const { data, isLoading, error } = useQuery({
    queryKey: ["users"],
    queryFn: () => fetch("/api/users").then((res) => res.json()),
  });

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;

  return (
    <div>
      {data.map((user) => (
        <div key={user.id}>{user.name}</div>
      ))}
    </div>
  );
}
```

## 🌐 REST API

REST (Representational State Transfer) là kiến trúc API phổ biến nhất:

- **GET**: Lấy dữ liệu
- **POST**: Tạo mới
- **PUT/PATCH**: Cập nhật
- **DELETE**: Xóa

## ⚠️ Error Handling

```javascript
async function fetchData() {
  try {
    const response = await fetch("/api/data");
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Error fetching data:", error);
    // Handle error
  }
}
```

## 🔐 Authentication

```javascript
// JWT Token
const token = localStorage.getItem("token");

fetch("/api/protected", {
  headers: {
    Authorization: `Bearer ${token}`,
  },
});
```

## 💪 Thực hành

1. Tạo app hiển thị dữ liệu từ API
2. Xây dựng form gửi dữ liệu lên API
3. Xử lý loading và error states
4. Implement authentication

## 🔗 Tài nguyên

- [MDN Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [Axios Documentation](https://axios-http.com/)
- [React Query](https://tanstack.com/query/latest)

## ➡️ Bước tiếp theo

Sau khi nắm vững API Integration, hãy học [Build Tools](../build-tools/)!
