---
title: "JavaScript cơ bản"
date: 2025-01-20
description: "Học JavaScript từ đầu - Ngôn ngữ lập trình cho web"
weight: 3
---

# JavaScript cơ bản

JavaScript là ngôn ngữ lập trình phổ biến nhất trên thế giới, được sử dụng để tạo tương tác và logic cho các trang web.

## 💻 JavaScript là gì?

JavaScript là ngôn ngữ lập trình động, được thiết kế để tạo các trang web tương tác. Nó chạy trên trình duyệt và có thể thao tác với HTML và CSS.

### 🎯 Tại sao học JavaScript?

- 🌐 Ngôn ngữ phổ biến nhất cho web
- 🔄 Có thể chạy trên cả frontend và backend (Node.js)
- 👥 Cộng đồng lớn và tài nguyên phong phú
- 📦 Nhiều framework và thư viện mạnh mẽ

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/UGFaM0sT-0g" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/JavaScriptCoBan.jpg" alt="JavaScript cơ bản" />

## 📚 Nội dung cần học

### Cơ bản

- Biến (var, let, const)
- Kiểu dữ liệu (string, number, boolean, object, array)
- Operators (+, -, \*, /, ===, !==)
- Conditional statements (if, else, switch)
- Loops (for, while, forEach)
- Functions
- Scope và hoisting

### DOM Manipulation

- Truy cập elements (getElementById, querySelector)
- Thay đổi nội dung
- Thêm/xóa elements
- Event listeners
- Event handling

### Arrays và Objects

- Array methods (map, filter, reduce)
- Object methods
- Destructuring
- Spread operator

## 💡 Ví dụ code

```javascript
// Biến và kiểu dữ liệu
let name = "Phạm Tùng Dương";
const age = 21;
var isStudent = true;

// Function
function greet(name) {
  return `Xin chào, ${name}!`;
}

// DOM Manipulation
document.getElementById("button").addEventListener("click", function () {
  alert("Button clicked!");
});

// Array methods
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((n) => n * 2);
```

## 💪 Thực hành

1. 🧮 Tạo calculator đơn giản
2. ✅ Xây dựng todo list
3. 📝 Tạo form validation
4. 🖼️ Xây dựng image slider

## 🔗 Tài nguyên

- [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [JavaScript.info](https://javascript.info/)
- [freeCodeCamp JavaScript](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)

## ➡️ Bước tiếp theo

Sau khi nắm vững JavaScript cơ bản, hãy học [Responsive Design](../responsive-design/)!
