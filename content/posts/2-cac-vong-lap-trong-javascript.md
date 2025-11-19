---
title: "Các Vòng Lặp Trong JavaScript"
date: 2025-01-12
category: "javascript"
tags: ["JavaScript", "Vòng lặp", "ES6", "Lập trình cơ bản"]
summary: "Khám phá các loại vòng lặp trong JavaScript: for, while, do-while, for...of, for...in và forEach với ví dụ thực tế."
---

Vòng lặp là cấu trúc điều khiển quan trọng giúp thực thi một khối mã nhiều lần. JavaScript cung cấp nhiều loại vòng lặp khác nhau, mỗi loại phù hợp với các tình huống cụ thể.

## 1. Vòng Lặp For

Vòng lặp `for` là phổ biến nhất, phù hợp khi bạn biết số lần lặp:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(`Lần lặp thứ ${i + 1}`);
}

// Output:
// Lần lặp thứ 1
// Lần lặp thứ 2
// Lần lặp thứ 3
// Lần lặp thứ 4
// Lần lặp thứ 5
```

### Vòng Lặp For Lồng Nhau

```javascript
for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        console.log(`i=${i}, j=${j}`);
    }
}
```

## 2. Vòng Lặp While

Vòng lặp `while` thực thi khi điều kiện còn đúng:

```javascript
let count = 0;
while (count < 5) {
    console.log(`Count: ${count}`);
    count++;
}
```

### Vòng Lặp While Vô Hạn (Cẩn Thận!)

```javascript
let running = true;
while (running) {
    // Thực hiện công việc
    if (someCondition) {
        running = false; // Thoát vòng lặp
    }
}
```

## 3. Vòng Lặp Do-While

Vòng lặp `do-while` thực thi ít nhất một lần:

```javascript
let x = 0;
do {
    console.log(`Giá trị: ${x}`);
    x++;
} while (x < 5);
```

## 4. Vòng Lặp For...Of (ES6)

Vòng lặp `for...of` duyệt qua các phần tử của mảng hoặc iterable:

```javascript
const fruits = ['Táo', 'Chuối', 'Cam'];
for (const fruit of fruits) {
    console.log(`Tôi thích ${fruit}`);
}

// Với chuỗi
const text = "Hello";
for (const char of text) {
    console.log(char);
}
```

## 5. Vòng Lặp For...In

Vòng lặp `for...in` duyệt qua các thuộc tính của object:

```javascript
const person = {
    name: 'Nguyễn Văn A',
    age: 25,
    job: 'Developer'
};

for (const key in person) {
    console.log(`${key}: ${person[key]}`);
}
```

## 6. Phương Thức ForEach

`forEach` là phương thức của mảng, nhận callback function:

```javascript
const numbers = [1, 2, 3, 4, 5];
numbers.forEach((num, index) => {
    console.log(`Số ${num} ở vị trí ${index}`);
});

// Với object
const users = [
    { name: 'An', age: 20 },
    { name: 'Bình', age: 25 }
];

users.forEach(user => {
    console.log(`${user.name} - ${user.age} tuổi`);
});
```

## 7. Các Phương Thức Lặp Khác

### Map - Tạo mảng mới từ mảng cũ

```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8]
```

### Filter - Lọc phần tử

```javascript
const numbers = [1, 2, 3, 4, 5, 6];
const evens = numbers.filter(num => num % 2 === 0);
console.log(evens); // [2, 4, 6]
```

### Reduce - Tổng hợp giá trị

```javascript
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 15
```

## So Sánh và Lựa Chọn

| Loại Vòng Lặp | Khi Nào Sử Dụng |
|---------------|-----------------|
| `for` | Biết số lần lặp, cần index |
| `while` | Điều kiện động, không biết số lần |
| `do-while` | Cần thực thi ít nhất 1 lần |
| `for...of` | Duyệt mảng/iterable, không cần index |
| `for...in` | Duyệt thuộc tính object |
| `forEach` | Duyệt mảng với callback, không return |
| `map/filter/reduce` | Xử lý và biến đổi mảng |

## Kết Luận

Mỗi loại vòng lặp có ưu điểm riêng. Hiểu rõ từng loại giúp bạn viết code hiệu quả và dễ đọc hơn. Trong lập trình mạng, vòng lặp thường được dùng để xử lý danh sách kết nối, dữ liệu từ API, hoặc các tác vụ bất đồng bộ.

