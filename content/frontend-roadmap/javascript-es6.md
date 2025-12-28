---
title: "JavaScript ES6+"
date: 2025-01-20
description: "Các tính năng hiện đại của JavaScript"
weight: 6
---

# JavaScript ES6+

ES6 (ECMAScript 2015) và các phiên bản sau đó đã mang đến nhiều tính năng mới mạnh mẽ cho JavaScript, giúp code ngắn gọn và dễ đọc hơn.

## ⚡ ES6+ là gì?

ES6+ bao gồm các tính năng JavaScript hiện đại từ ES6 (2015) trở đi, giúp viết code hiện đại và hiệu quả hơn.

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/rhi5bNOCiVo" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/JavaScriptES6.jpg" alt="JavaScript ES6+" />

## 📚 Các tính năng quan trọng

### 1. let và const

```javascript
// ES5
var name = "John";

// ES6+
let name = "John";  // Có thể thay đổi
const age = 25;     // Không thể thay đổi
```

### 2. Arrow Functions

```javascript
// ES5
function greet(name) {
    return "Hello " + name;
}

// ES6+
const greet = (name) => "Hello " + name;
```

### 3. Template Literals

```javascript
// ES5
var message = "Hello " + name + ", you are " + age + " years old";

// ES6+
const message = `Hello ${name}, you are ${age} years old`;
```

### 4. Destructuring

```javascript
// Array destructuring
const [first, second] = [1, 2];

// Object destructuring
const {name, age} = {name: "John", age: 25};
```

### 5. Spread Operator

```javascript
// Array
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];

// Object
const obj1 = {a: 1, b: 2};
const obj2 = {...obj1, c: 3};
```

### 6. Classes

```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    greet() {
        return `Hello, I'm ${this.name}`;
    }
}
```

### 7. Promises và Async/Await

```javascript
// Promises
fetch('/api/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error(error));

// Async/Await
async function getData() {
    try {
        const response = await fetch('/api/data');
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

### 8. Modules

```javascript
// export
export const name = "John";
export function greet() { return "Hello"; }

// import
import { name, greet } from './module.js';
```

## 💪 Thực hành

1. Refactor code cũ sang ES6+
2. Sử dụng async/await với API
3. Tạo và sử dụng modules
4. Áp dụng destructuring và spread operator

## 🔗 Tài nguyên

- [ES6 Features](https://es6-features.org/)
- [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)

## ➡️ Bước tiếp theo

Sau khi nắm vững ES6+, hãy học [Git & Version Control](../git-version-control/)!

