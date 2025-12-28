---
title: "React.js"
date: 2025-01-20
description: "Học React.js - Framework JavaScript phổ biến nhất"
weight: 8
---

# React.js

React là thư viện JavaScript mã nguồn mở được phát triển bởi Facebook, được sử dụng để xây dựng giao diện người dùng, đặc biệt là các ứng dụng web đơn trang (SPA).

## ⚛️ React là gì?

React cho phép bạn xây dựng các component có thể tái sử dụng và quản lý state một cách hiệu quả. Nó sử dụng Virtual DOM để tối ưu hiệu năng.

### Tại sao học React?

- Framework phổ biến nhất hiện nay
- Cộng đồng lớn và tài nguyên phong phú
- Nhiều cơ hội việc làm
- Được sử dụng bởi các công ty lớn (Facebook, Netflix, Airbnb)

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/s2skans2dP4" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/Reactjs.jpg" alt="React.js" />

## 📚 Các khái niệm cơ bản

### 1. Components

```jsx
// Functional Component
function Welcome(props) {
    return <h1>Hello, {props.name}!</h1>;
}

// Arrow Function Component
const Welcome = (props) => {
    return <h1>Hello, {props.name}!</h1>;
}
```

### 2. JSX

```jsx
const element = <h1>Hello, World!</h1>;
const name = "John";
const element = <h1>Hello, {name}!</h1>;
```

### 3. Props

```jsx
function UserCard({ name, email, avatar }) {
    return (
        <div className="user-card">
            <img src={avatar} alt={name} />
            <h2>{name}</h2>
            <p>{email}</p>
        </div>
    );
}
```

### 4. State với Hooks

```jsx
import { useState } from 'react';

function Counter() {
    const [count, setCount] = useState(0);
    
    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                Click me
            </button>
        </div>
    );
}
```

### 5. useEffect Hook

```jsx
import { useState, useEffect } from 'react';

function DataFetcher() {
    const [data, setData] = useState(null);
    
    useEffect(() => {
        fetch('/api/data')
            .then(res => res.json())
            .then(data => setData(data));
    }, []);
    
    return <div>{data && <p>{data.message}</p>}</div>;
}
```

## 📖 Nội dung cần học

- Components và JSX
- Props và State
- Hooks (useState, useEffect, useContext)
- Event Handling
- Conditional Rendering
- Lists và Keys
- Forms
- React Router
- Context API

## 💪 Thực hành

1. Tạo Todo App với React
2. Xây dựng Weather App
3. Tạo Blog với React Router
4. Build E-commerce product page

## 🔗 Tài nguyên

- [React Official Documentation](https://react.dev/)
- [React Tutorial](https://react.dev/learn)
- [freeCodeCamp React](https://www.freecodecamp.org/learn/front-end-development-libraries/)

## ➡️ Bước tiếp theo

Sau khi nắm vững React, hãy học [State Management](../state-management/)!

