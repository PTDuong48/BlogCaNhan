---
title: "DOM Manipulation Trong JavaScript"
date: 2025-01-03
category: "javascript"
tags: ["JavaScript", "DOM", "Frontend", "Web Development", "HTML"]
summary: "Học cách thao tác với DOM (Document Object Model) trong JavaScript: thêm, sửa, xóa elements, xử lý events và tối ưu hiệu suất."
image: "/images/DomJavaScript.jpg"
---

DOM (Document Object Model) là biểu diễn cấu trúc HTML của trang web. JavaScript cho phép bạn thao tác với DOM để tạo ra các trang web động và tương tác.

## Lấy Elements

### getElementById

```javascript
const element = document.getElementById('myId');
console.log(element);
```

### querySelector và querySelectorAll

```javascript
// Lấy element đầu tiên
const firstDiv = document.querySelector('.my-class');
const firstButton = document.querySelector('button');

// Lấy tất cả elements
const allDivs = document.querySelectorAll('.my-class');
const allButtons = document.querySelectorAll('button');
```

### getElementsByClassName và getElementsByTagName

```javascript
const elements = document.getElementsByClassName('my-class');
const divs = document.getElementsByTagName('div');
```

## Tạo Elements

```javascript
// Tạo element mới
const newDiv = document.createElement('div');
newDiv.textContent = 'Nội dung mới';
newDiv.className = 'my-class';
newDiv.id = 'new-id';

// Thêm vào DOM
document.body.appendChild(newDiv);
```

### Tạo Element với Attributes

```javascript
const link = document.createElement('a');
link.href = 'https://example.com';
link.textContent = 'Click me';
link.target = '_blank';
link.setAttribute('data-id', '123');

document.body.appendChild(link);
```

## Thêm và Xóa Elements

### appendChild và insertBefore

```javascript
const parent = document.getElementById('parent');
const newElement = document.createElement('div');
newElement.textContent = 'Element mới';

// Thêm vào cuối
parent.appendChild(newElement);

// Thêm vào trước element khác
const existingElement = document.getElementById('existing');
parent.insertBefore(newElement, existingElement);
```

### removeChild và remove

```javascript
const parent = document.getElementById('parent');
const child = document.getElementById('child');

// Cách 1: Sử dụng removeChild
parent.removeChild(child);

// Cách 2: Sử dụng remove (hiện đại hơn)
child.remove();
```

### replaceChild

```javascript
const parent = document.getElementById('parent');
const oldElement = document.getElementById('old');
const newElement = document.createElement('div');
newElement.textContent = 'Element mới';

parent.replaceChild(newElement, oldElement);
```

## Thay Đổi Nội Dung

### textContent và innerHTML

```javascript
const element = document.getElementById('myElement');

// textContent - chỉ text, an toàn hơn
element.textContent = 'Nội dung mới';

// innerHTML - cho phép HTML, cẩn thận với XSS
element.innerHTML = '<strong>Nội dung</strong> với <em>HTML</em>';
```

### innerText vs textContent

```javascript
// textContent - lấy tất cả text, kể cả ẩn
const text1 = element.textContent;

// innerText - chỉ lấy text hiển thị
const text2 = element.innerText;
```

## Thay Đổi Attributes và Styles

### Attributes

```javascript
const element = document.getElementById('myElement');

// Đọc attribute
const id = element.getAttribute('id');
const dataValue = element.getAttribute('data-value');

// Ghi attribute
element.setAttribute('class', 'new-class');
element.setAttribute('data-id', '123');

// Xóa attribute
element.removeAttribute('data-id');

// Đọc/ghi thuộc tính trực tiếp
element.id = 'new-id';
element.className = 'new-class';
```

### Styles

```javascript
const element = document.getElementById('myElement');

// Thay đổi style trực tiếp
element.style.color = 'red';
element.style.backgroundColor = 'blue';
element.style.fontSize = '20px';
element.style.display = 'none';

// Thêm/xóa class
element.classList.add('active');
element.classList.remove('inactive');
element.classList.toggle('highlight');
element.classList.replace('old-class', 'new-class');

// Kiểm tra class
if (element.classList.contains('active')) {
    console.log('Element có class active');
}
```

## Xử Lý Events

### addEventListener

```javascript
const button = document.getElementById('myButton');

button.addEventListener('click', function(event) {
    console.log('Button được click!');
    console.log('Event:', event);
    console.log('Target:', event.target);
});
```

### Event Delegation

```javascript
// Thay vì thêm listener cho từng button
const container = document.getElementById('container');

container.addEventListener('click', function(event) {
    if (event.target.classList.contains('button')) {
        console.log('Button được click:', event.target.textContent);
    }
});
```

### Các Events Phổ Biến

```javascript
const element = document.getElementById('myElement');

// Click
element.addEventListener('click', handleClick);

// Mouse events
element.addEventListener('mouseenter', () => console.log('Mouse enter'));
element.addEventListener('mouseleave', () => console.log('Mouse leave'));
element.addEventListener('mousemove', (e) => console.log('Mouse move', e.clientX, e.clientY));

// Keyboard events
document.addEventListener('keydown', (e) => {
    console.log('Key pressed:', e.key);
    if (e.key === 'Enter') {
        console.log('Enter được nhấn');
    }
});

// Form events
const form = document.getElementById('myForm');
form.addEventListener('submit', (e) => {
    e.preventDefault(); // Ngăn submit mặc định
    console.log('Form submitted');
});

// Input events
const input = document.getElementById('myInput');
input.addEventListener('input', (e) => {
    console.log('Input value:', e.target.value);
});
```

## Traversing DOM

```javascript
const element = document.getElementById('myElement');

// Parent
const parent = element.parentElement;
const parentNode = element.parentNode;

// Children
const firstChild = element.firstElementChild;
const lastChild = element.lastElementChild;
const children = element.children;

// Siblings
const nextSibling = element.nextElementSibling;
const previousSibling = element.previousElementSibling;

// Tất cả siblings
const siblings = Array.from(element.parentElement.children)
    .filter(child => child !== element);
```

## Ví Dụ Thực Tế: Tạo Todo List

```javascript
// HTML: <ul id="todoList"></ul>

const todoList = document.getElementById('todoList');
const input = document.getElementById('todoInput');
const addButton = document.getElementById('addButton');

function addTodo() {
    const text = input.value.trim();
    if (text === '') return;
    
    // Tạo li element
    const li = document.createElement('li');
    li.className = 'todo-item';
    
    // Tạo span cho text
    const span = document.createElement('span');
    span.textContent = text;
    
    // Tạo button xóa
    const deleteBtn = document.createElement('button');
    deleteBtn.textContent = 'Xóa';
    deleteBtn.addEventListener('click', () => {
        li.remove();
    });
    
    // Thêm vào DOM
    li.appendChild(span);
    li.appendChild(deleteBtn);
    todoList.appendChild(li);
    
    // Xóa input
    input.value = '';
}

addButton.addEventListener('click', addTodo);
input.addEventListener('keypress', (e) => {
    if (e.key === 'Enter') {
        addTodo();
    }
});
```

## Tối Ưu Hiệu Suất

### 1. Sử dụng DocumentFragment

```javascript
const fragment = document.createDocumentFragment();

for (let i = 0; i < 1000; i++) {
    const div = document.createElement('div');
    div.textContent = `Item ${i}`;
    fragment.appendChild(div);
}

document.body.appendChild(fragment); // Chỉ reflow một lần
```

### 2. Batch DOM Updates

```javascript
// ❌ Bad - Nhiều reflow
element.style.width = '100px';
element.style.height = '100px';
element.style.backgroundColor = 'red';

// ✅ Good - Một reflow
element.style.cssText = 'width: 100px; height: 100px; background-color: red;';
```

### 3. Debounce và Throttle

```javascript
function debounce(func, wait) {
    let timeout;
    return function executedFunction(...args) {
        const later = () => {
            clearTimeout(timeout);
            func(...args);
        };
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
    };
}

const handleScroll = debounce(() => {
    console.log('Scrolling...');
}, 200);

window.addEventListener('scroll', handleScroll);
```

## Kết Luận

DOM Manipulation là kỹ năng cơ bản nhưng mạnh mẽ trong JavaScript. Hiểu rõ cách thao tác với DOM giúp bạn tạo ra các trang web tương tác và động. Trong lập trình mạng, DOM thường được sử dụng để hiển thị dữ liệu từ API, cập nhật giao diện real-time, và xử lý user interactions.

