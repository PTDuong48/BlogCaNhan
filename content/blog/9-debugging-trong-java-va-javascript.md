---
title: "Debugging Trong Java & JavaScript"
date: 2024-12-28
category: "java"
tags: ["Java", "JavaScript", "Debugging", "Development", "Tools"]
summary: "Hướng dẫn kỹ thuật debugging hiệu quả trong Java và JavaScript: sử dụng debugger, logging, breakpoints và các công cụ hỗ trợ."
image: "/images/Debugging.png"
---

Debugging là kỹ năng quan trọng trong phát triển phần mềm. Bài viết này sẽ hướng dẫn bạn các kỹ thuật debugging hiệu quả cho cả Java và JavaScript.

## Debugging trong Java

### 1. Sử dụng System.out.println

Cách đơn giản nhất để debug:

```java
public class DebugExample {
    public static void main(String[] args) {
        int x = 10;
        System.out.println("Giá trị x: " + x);
        
        int result = calculate(x);
        System.out.println("Kết quả: " + result);
    }
    
    private static int calculate(int value) {
        System.out.println("Đang tính với giá trị: " + value);
        return value * 2;
    }
}
```

### 2. Sử dụng Logger (Khuyến nghị)

```java
import java.util.logging.Logger;
import java.util.logging.Level;

public class LoggerExample {
    private static final Logger logger = Logger.getLogger(LoggerExample.class.getName());
    
    public static void main(String[] args) {
        logger.info("Ứng dụng bắt đầu");
        logger.warning("Cảnh báo: Giá trị có thể null");
        logger.severe("Lỗi nghiêm trọng!");
        
        try {
            int result = divide(10, 0);
        } catch (ArithmeticException e) {
            logger.log(Level.SEVERE, "Lỗi chia cho 0", e);
        }
    }
    
    private static int divide(int a, int b) {
        logger.fine("Thực hiện phép chia: " + a + " / " + b);
        return a / b;
    }
}
```

### 3. Debugger trong IntelliJ IDEA

#### Thiết lập Breakpoint

1. Click vào gutter (bên trái số dòng) để đặt breakpoint
2. Chạy ở chế độ Debug (Shift + F9)
3. Sử dụng các nút:
   - **F8 (Step Over):** Chạy dòng hiện tại
   - **F7 (Step Into):** Vào bên trong function
   - **Shift + F8 (Step Out):** Thoát khỏi function
   - **F9 (Resume):** Tiếp tục chạy

#### Xem Variables

```java
public class DebugExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};
        int sum = 0;
        
        for (int i = 0; i < numbers.length; i++) {
            sum += numbers[i]; // Đặt breakpoint ở đây
            // Xem giá trị của i, numbers[i], sum trong debugger
        }
        
        System.out.println("Tổng: " + sum);
    }
}
```

#### Conditional Breakpoint

```java
for (int i = 0; i < 100; i++) {
    process(i); // Breakpoint chỉ dừng khi i > 50
}
```

### 4. Debugging với Eclipse

Tương tự IntelliJ, Eclipse cũng có debugger mạnh mẽ:
- Đặt breakpoint: Double-click gutter
- Debug: F11
- Step Over: F6
- Step Into: F5
- Resume: F8

### 5. Remote Debugging

Debug ứng dụng chạy trên server từ xa:

```bash
# Khởi chạy Java với remote debugging
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 MyApp
```

Trong IDE, kết nối đến `localhost:5005`.

## Debugging trong JavaScript

### 1. Console Methods

```javascript
// console.log - In thông tin
console.log('Giá trị:', value);
console.log('Object:', obj);

// console.error - In lỗi
console.error('Lỗi xảy ra:', error);

// console.warn - Cảnh báo
console.warn('Cảnh báo: Giá trị không hợp lệ');

// console.table - Hiển thị dạng bảng
const users = [
    { name: 'An', age: 20 },
    { name: 'Bình', age: 25 }
];
console.table(users);

// console.group - Nhóm logs
console.group('API Calls');
console.log('Request 1');
console.log('Request 2');
console.groupEnd();

// console.time - Đo thời gian
console.time('fetchData');
await fetchData();
console.timeEnd('fetchData');
```

### 2. Debugger Statement

```javascript
function processData(data) {
    debugger; // Dừng tại đây nếu DevTools mở
    const result = data.map(item => item * 2);
    return result;
}
```

### 3. Chrome DevTools

#### Breakpoints

1. Mở DevTools (F12)
2. Vào tab Sources
3. Click vào số dòng để đặt breakpoint
4. Reload trang
5. Sử dụng controls:
   - **F8:** Resume
   - **F10:** Step over
   - **F11:** Step into
   - **Shift + F11:** Step out

#### Watch Expressions

Theo dõi giá trị biến trong quá trình debug:

```javascript
let x = 10;
let y = 20;
let sum = x + y; // Đặt breakpoint ở đây
// Thêm 'x', 'y', 'sum' vào Watch panel
```

#### Call Stack

Xem chuỗi function calls dẫn đến breakpoint.

### 4. VS Code Debugging

Tạo file `.vscode/launch.json`:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Debug Node.js",
            "program": "${workspaceFolder}/app.js",
            "skipFiles": ["<node_internals>/**"]
        },
        {
            "type": "chrome",
            "request": "launch",
            "name": "Debug Chrome",
            "url": "http://localhost:3000",
            "webRoot": "${workspaceFolder}"
        }
    ]
}
```

### 5. Network Debugging

```javascript
// Log tất cả fetch requests
const originalFetch = window.fetch;
window.fetch = function(...args) {
    console.log('Fetch request:', args[0]);
    return originalFetch.apply(this, args)
        .then(response => {
            console.log('Fetch response:', response);
            return response;
        });
};

// Sử dụng
fetch('/api/data')
    .then(res => res.json())
    .then(data => console.log(data));
```

## Kỹ Thuật Debugging Chung

### 1. Binary Search Debugging

Chia code thành các phần nhỏ để tìm lỗi:

```java
// Thay vì debug toàn bộ function
public int complexCalculation(int[] data) {
    // Đặt breakpoint ở giữa
    int step1 = processStep1(data);
    // Kiểm tra step1 đúng chưa
    int step2 = processStep2(step1);
    // Kiểm tra step2 đúng chưa
    return step3(step2);
}
```

### 2. Logging Levels

```java
// Java với Log4j
import org.apache.log4j.Logger;
import org.apache.log4j.Level;

Logger logger = Logger.getLogger(MyClass.class);
logger.setLevel(Level.DEBUG);

logger.debug("Chi tiết debug");
logger.info("Thông tin");
logger.warn("Cảnh báo");
logger.error("Lỗi");
```

```javascript
// JavaScript với custom logger
const logger = {
    debug: (msg) => console.log('[DEBUG]', msg),
    info: (msg) => console.log('[INFO]', msg),
    warn: (msg) => console.warn('[WARN]', msg),
    error: (msg) => console.error('[ERROR]', msg)
};
```

### 3. Assertions

```java
// Java
assert condition : "Điều kiện không đúng";
```

```javascript
// JavaScript
console.assert(condition, "Điều kiện không đúng");

// Hoặc throw error
if (!condition) {
    throw new Error("Điều kiện không đúng");
}
```

### 4. Unit Testing như Debugging Tool

```java
// JUnit test giúp tìm lỗi
@Test
public void testCalculation() {
    int result = calculate(10, 5);
    assertEquals(15, result);
}
```

```javascript
// Jest test
test('should calculate correctly', () => {
    const result = calculate(10, 5);
    expect(result).toBe(15);
});
```

## Debugging Network Issues

### Java

```java
// Log HTTP requests
System.setProperty("javax.net.debug", "all");

// Hoặc sử dụng logging interceptor
public class LoggingInterceptor implements ClientHttpRequestInterceptor {
    @Override
    public ClientHttpResponse intercept(
            HttpRequest request, 
            byte[] body, 
            ClientHttpRequestExecution execution) throws IOException {
        System.out.println("Request: " + request.getURI());
        System.out.println("Body: " + new String(body));
        return execution.execute(request, body);
    }
}
```

### JavaScript

```javascript
// Sử dụng Network tab trong DevTools
// Hoặc log requests
const originalXHR = window.XMLHttpRequest;
window.XMLHttpRequest = function() {
    const xhr = new originalXHR();
    xhr.addEventListener('load', function() {
        console.log('XHR Response:', this.responseText);
    });
    return xhr;
};
```

## Best Practices

1. **Sử dụng debugger thay vì console.log:** Hiệu quả hơn
2. **Đặt breakpoint có điều kiện:** Tiết kiệm thời gian
3. **Sử dụng logging framework:** Thay vì System.out.println
4. **Viết unit tests:** Giúp tìm lỗi sớm
5. **Đọc stack trace:** Hiểu rõ lỗi xảy ra ở đâu
6. **Sử dụng version control:** So sánh code để tìm thay đổi gây lỗi

## Kết Luận

Debugging là kỹ năng cần thiết cho mọi developer. Hiểu rõ các công cụ và kỹ thuật debugging giúp bạn tìm và sửa lỗi nhanh chóng, đặc biệt trong lập trình mạng nơi có nhiều tương tác phức tạp giữa client và server.

