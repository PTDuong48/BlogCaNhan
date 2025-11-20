---
title: "Event Loop Trong JavaScript"
date: 2025-01-08
category: "javascript"
tags: ["JavaScript", "Event Loop", "Async", "Concurrency", "Node.js"]
summary: "Tìm hiểu về Event Loop - cơ chế xử lý bất đồng bộ trong JavaScript, cách hoạt động và ứng dụng trong lập trình mạng."
image: "/images/EventloopJava.jpg"
---

Event Loop là một trong những khái niệm quan trọng nhất trong JavaScript, đặc biệt khi làm việc với lập trình mạng và xử lý bất đồng bộ. Hãy cùng khám phá cách nó hoạt động.

## Event Loop Là Gì?

Event Loop là cơ chế cho phép JavaScript xử lý các tác vụ bất đồng bộ mà không chặn luồng chính. Nó giúp JavaScript có thể xử lý nhiều tác vụ đồng thời mặc dù là ngôn ngữ single-threaded.

## Call Stack và Callback Queue

### Call Stack

Call Stack là nơi lưu trữ các function đang được thực thi:

```javascript
function first() {
    console.log('First');
    second();
}

function second() {
    console.log('Second');
    third();
}

function third() {
    console.log('Third');
}

first();
// Output: First, Second, Third
```

### Callback Queue

Callback Queue chứa các callback function chờ được thực thi:

```javascript
console.log('Start');

setTimeout(() => {
    console.log('Timeout 1');
}, 0);

setTimeout(() => {
    console.log('Timeout 2');
}, 0);

console.log('End');

// Output: Start, End, Timeout 1, Timeout 2
```

## Cách Event Loop Hoạt Động

```javascript
console.log('1');

setTimeout(() => {
    console.log('2');
}, 0);

Promise.resolve().then(() => {
    console.log('3');
});

console.log('4');

// Output: 1, 4, 3, 2
```

**Giải thích:**
1. `console.log('1')` - thực thi ngay
2. `setTimeout` - đưa vào Web APIs, sau đó vào Callback Queue
3. `Promise.resolve()` - đưa vào Microtask Queue (ưu tiên cao hơn)
4. `console.log('4')` - thực thi ngay
5. Event Loop kiểm tra Microtask Queue trước → in '3'
6. Sau đó mới xử lý Callback Queue → in '2'

## Microtask Queue vs Callback Queue

### Microtask Queue (Ưu tiên cao)

```javascript
Promise.resolve().then(() => console.log('Microtask 1'));
Promise.resolve().then(() => console.log('Microtask 2'));
```

### Callback Queue (Ưu tiên thấp)

```javascript
setTimeout(() => console.log('Callback 1'), 0);
setTimeout(() => console.log('Callback 2'), 0);
```

## Async/Await và Event Loop

```javascript
async function example() {
    console.log('1');
    
    await Promise.resolve();
    console.log('2');
    
    await new Promise(resolve => setTimeout(resolve, 0));
    console.log('3');
}

example();
console.log('4');

// Output: 1, 4, 2, 3
```

## Ứng Dụng Trong Lập Trình Mạng

### Fetch API

```javascript
console.log('Bắt đầu request');

fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => {
        console.log('Nhận được dữ liệu:', data);
    })
    .catch(error => {
        console.error('Lỗi:', error);
    });

console.log('Request đã gửi');

// Output:
// Bắt đầu request
// Request đã gửi
// Nhận được dữ liệu: {...}
```

### Xử Lý Nhiều Request Đồng Thời

```javascript
async function fetchMultiple() {
    console.log('Bắt đầu fetch');
    
    const promises = [
        fetch('https://api.example.com/data1'),
        fetch('https://api.example.com/data2'),
        fetch('https://api.example.com/data3')
    ];
    
    const results = await Promise.all(promises);
    console.log('Tất cả request đã hoàn thành');
    
    return results;
}

fetchMultiple();
```

## Node.js Event Loop

Trong Node.js, Event Loop có các phase:

1. **Timer:** Xử lý setTimeout và setInterval
2. **Pending callbacks:** Xử lý I/O callbacks bị trì hoãn
3. **Idle, prepare:** Chỉ sử dụng nội bộ
4. **Poll:** Lấy sự kiện mới, thực thi I/O callbacks
5. **Check:** Xử lý setImmediate callbacks
6. **Close callbacks:** Xử lý close events

```javascript
// Node.js example
const fs = require('fs');

console.log('Start');

fs.readFile('file.txt', (err, data) => {
    console.log('File read complete');
});

setImmediate(() => {
    console.log('setImmediate');
});

setTimeout(() => {
    console.log('setTimeout');
}, 0);

Promise.resolve().then(() => {
    console.log('Promise');
});

console.log('End');
```

## Best Practices

1. **Tránh blocking Event Loop:**
```javascript
// ❌ Bad - Blocking
for (let i = 0; i < 1000000000; i++) {
    // Heavy computation
}

// ✅ Good - Non-blocking
function processChunk(start, end) {
    for (let i = start; i < end; i++) {
        // Process
    }
    if (end < 1000000000) {
        setImmediate(() => processChunk(end, end + 1000));
    }
}
```

2. **Sử dụng Promise.all cho parallel tasks:**
```javascript
// ✅ Good
const results = await Promise.all([
    fetchData1(),
    fetchData2(),
    fetchData3()
]);
```

3. **Xử lý lỗi đúng cách:**
```javascript
try {
    const data = await fetchData();
} catch (error) {
    console.error('Error:', error);
}
```

## Kết Luận

Hiểu rõ Event Loop giúp bạn viết code JavaScript hiệu quả hơn, đặc biệt trong lập trình mạng nơi có nhiều tác vụ bất đồng bộ. Nó là nền tảng cho việc xử lý API calls, WebSocket connections, và các tác vụ I/O khác.

