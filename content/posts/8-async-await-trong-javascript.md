---
title: "Async/Await Trong JavaScript"
date: 2024-12-30
category: "javascript"
tags: ["JavaScript", "Async", "Await", "Promise", "ES6"]
summary: "Tìm hiểu về async/await - cú pháp hiện đại để xử lý bất đồng bộ trong JavaScript, cách sử dụng và best practices."
---

Async/await là cú pháp được giới thiệu trong ES2017, giúp viết code bất đồng bộ dễ đọc và dễ hiểu hơn so với Promise chains. Đây là công cụ mạnh mẽ trong lập trình mạng với JavaScript.

## Async Function

Hàm `async` luôn trả về một Promise:

```javascript
async function fetchData() {
  return "Dữ liệu";
}

// Tương đương với:
function fetchData() {
  return Promise.resolve("Dữ liệu");
}

// Sử dụng
fetchData().then((data) => console.log(data));
```

## Await Keyword

`await` chỉ có thể sử dụng bên trong hàm `async`. Nó chờ Promise resolve trước khi tiếp tục:

```javascript
async function example() {
  const data = await fetchData();
  console.log(data); // Chạy sau khi fetchData() hoàn thành
}
```

## So Sánh Promise và Async/Await

### Sử dụng Promise (Callback Hell)

```javascript
function getUserData(userId) {
  return fetch(`/api/users/${userId}`)
    .then((response) => response.json())
    .then((user) => {
      return fetch(`/api/posts/${user.id}`)
        .then((response) => response.json())
        .then((posts) => {
          return { user, posts };
        });
    })
    .catch((error) => {
      console.error("Lỗi:", error);
    });
}
```

### Sử dụng Async/Await (Dễ đọc hơn)

```javascript
async function getUserData(userId) {
  try {
    const userResponse = await fetch(`/api/users/${userId}`);
    const user = await userResponse.json();

    const postsResponse = await fetch(`/api/posts/${user.id}`);
    const posts = await postsResponse.json();

    return { user, posts };
  } catch (error) {
    console.error("Lỗi:", error);
  }
}
```

## Xử Lý Lỗi

### Try-Catch

```javascript
async function fetchUserData() {
  try {
    const response = await fetch("/api/user");
    if (!response.ok) {
      throw new Error("HTTP error! status: " + response.status);
    }
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Lỗi fetch:", error);
    throw error; // Re-throw để caller xử lý
  }
}
```

### Kết Hợp với .catch()

```javascript
async function example() {
  const data = await fetchData().catch((error) => {
    console.error("Lỗi:", error);
    return null; // Giá trị mặc định
  });

  if (data) {
    console.log("Dữ liệu:", data);
  }
}
```

## Xử Lý Nhiều Promises

### Tuần Tự (Sequential)

```javascript
async function processSequentially() {
  const result1 = await fetchData1();
  const result2 = await fetchData2();
  const result3 = await fetchData3();

  return { result1, result2, result3 };
}
```

### Song Song (Parallel)

```javascript
async function processParallel() {
  // Tất cả promises chạy đồng thời
  const [result1, result2, result3] = await Promise.all([
    fetchData1(),
    fetchData2(),
    fetchData3(),
  ]);

  return { result1, result2, result3 };
}
```

### Promise.allSettled (Không dừng khi có lỗi)

```javascript
async function processAllSettled() {
  const results = await Promise.allSettled([
    fetchData1(),
    fetchData2(),
    fetchData3(),
  ]);

  results.forEach((result, index) => {
    if (result.status === "fulfilled") {
      console.log(`Request ${index + 1} thành công:`, result.value);
    } else {
      console.log(`Request ${index + 1} thất bại:`, result.reason);
    }
  });
}
```

### Promise.race (Lấy kết quả đầu tiên)

```javascript
async function getFastestResponse() {
  const result = await Promise.race([
    fetch("/api/slow"),
    fetch("/api/fast"),
    fetch("/api/medium"),
  ]);

  return result.json();
}
```

## Async/Await với Loops

### For Loop (Tuần Tự)

```javascript
async function processArray(array) {
  const results = [];
  for (const item of array) {
    const result = await processItem(item);
    results.push(result);
  }
  return results;
}
```

### Map với Promise.all (Song Song)

```javascript
async function processArrayParallel(array) {
  const promises = array.map((item) => processItem(item));
  const results = await Promise.all(promises);
  return results;
}
```

## Ví Dụ Thực Tế: API Client

```javascript
class ApiClient {
  constructor(baseURL) {
    this.baseURL = baseURL;
  }

  async get(endpoint) {
    try {
      const response = await fetch(`${this.baseURL}${endpoint}`);
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      return await response.json();
    } catch (error) {
      console.error("GET error:", error);
      throw error;
    }
  }

  async post(endpoint, data) {
    try {
      const response = await fetch(`${this.baseURL}${endpoint}`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      });

      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }

      return await response.json();
    } catch (error) {
      console.error("POST error:", error);
      throw error;
    }
  }
}

// Sử dụng
const api = new ApiClient("https://api.example.com");

async function fetchUserPosts(userId) {
  try {
    const user = await api.get(`/users/${userId}`);
    const posts = await api.get(`/users/${userId}/posts`);

    return { user, posts };
  } catch (error) {
    console.error("Lỗi fetch user posts:", error);
    return null;
  }
}
```

## Async/Await với Timeout

```javascript
function timeout(ms) {
  return new Promise((_, reject) =>
    setTimeout(() => reject(new Error("Timeout")), ms)
  );
}

async function fetchWithTimeout(url, timeoutMs = 5000) {
  try {
    const response = await Promise.race([fetch(url), timeout(timeoutMs)]);
    return await response.json();
  } catch (error) {
    if (error.message === "Timeout") {
      console.error("Request timeout");
    } else {
      console.error("Request failed:", error);
    }
    throw error;
  }
}
```

## Async Function trong Class

```javascript
class DataService {
  constructor(apiUrl) {
    this.apiUrl = apiUrl;
  }

  async fetchData() {
    const response = await fetch(this.apiUrl);
    return await response.json();
  }

  async saveData(data) {
    const response = await fetch(this.apiUrl, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(data),
    });
    return await response.json();
  }
}

// Sử dụng
const service = new DataService("https://api.example.com/data");

async function main() {
  const data = await service.fetchData();
  console.log("Data:", data);
}
```

## Best Practices

1. **Luôn sử dụng try-catch:** Xử lý lỗi đúng cách
2. **Sử dụng Promise.all cho parallel tasks:** Tăng hiệu suất
3. **Tránh await trong loops không cần thiết:** Sử dụng Promise.all
4. **Kiểm tra response.ok:** Trước khi parse JSON
5. **Không quên await:** Nếu không sẽ nhận Promise object
6. **Sử dụng async/await thay vì .then():** Code dễ đọc hơn

## Common Mistakes

### Quên await

```javascript
// ❌ Bad
async function example() {
  const data = fetchData(); // Nhận Promise, không phải data
  console.log(data); // [object Promise]
}

// ✅ Good
async function example() {
  const data = await fetchData();
  console.log(data); // Actual data
}
```

### Await trong forEach

```javascript
// ❌ Bad - forEach không chờ async
array.forEach(async (item) => {
  await processItem(item);
});

// ✅ Good - Sử dụng for...of
for (const item of array) {
  await processItem(item);
}

// ✅ Better - Parallel với Promise.all
await Promise.all(array.map((item) => processItem(item)));
```

## Kết Luận

Async/await làm cho code bất đồng bộ dễ đọc và dễ bảo trì hơn. Trong lập trình mạng, nó đặc biệt hữu ích khi làm việc với APIs, WebSocket, và các tác vụ I/O khác. Kết hợp với Promise.all và Promise.race, bạn có thể xây dựng các ứng dụng mạng hiệu quả và mạnh mẽ.
