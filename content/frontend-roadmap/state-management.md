---
title: "State Management"
date: 2025-01-20
description: "Quản lý state trong ứng dụng React"
weight: 9
---

# State Management

Quản lý state là một phần quan trọng trong phát triển ứng dụng React, đặc biệt khi ứng dụng trở nên phức tạp.

## 🔄 State Management là gì?

State Management là cách bạn quản lý và chia sẻ dữ liệu giữa các component trong ứng dụng. Khi ứng dụng lớn, việc quản lý state trở nên phức tạp.

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/J52I0bwAr8c" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/StateManagement.jpg" alt="State Management" />

## 📚 Các phương pháp quản lý state

### 1. Local State (useState)

```jsx
import { useState } from 'react';

function Counter() {
    const [count, setCount] = useState(0);
    return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

### 2. Context API

```jsx
import { createContext, useContext, useState } from 'react';

const ThemeContext = createContext();

function ThemeProvider({ children }) {
    const [theme, setTheme] = useState('light');
    return (
        <ThemeContext.Provider value={{ theme, setTheme }}>
            {children}
        </ThemeContext.Provider>
    );
}

function useTheme() {
    return useContext(ThemeContext);
}
```

### 3. Redux

```jsx
import { createStore } from 'redux';

// Reducer
function counter(state = 0, action) {
    switch (action.type) {
        case 'INCREMENT':
            return state + 1;
        case 'DECREMENT':
            return state - 1;
        default:
            return state;
    }
}

// Store
const store = createStore(counter);
```

### 4. Zustand (Lightweight)

```jsx
import create from 'zustand';

const useStore = create((set) => ({
    count: 0,
    increment: () => set((state) => ({ count: state.count + 1 })),
}));
```

## 💡 Khi nào dùng gì?

- **useState**: State local trong component
- **Context API**: State cần chia sẻ giữa vài component
- **Redux**: Ứng dụng lớn, state phức tạp
- **Zustand**: Cần giải pháp nhẹ hơn Redux

## ✅ Best Practices

- Giữ state gần nơi sử dụng nhất
- Tránh prop drilling với Context API
- Sử dụng Redux cho ứng dụng lớn
- Tách business logic ra khỏi components

## 💪 Thực hành

1. Quản lý state với Context API
2. Xây dựng app với Redux
3. So sánh các phương pháp
4. Tối ưu performance

## 🔗 Tài nguyên

- [React Context API](https://react.dev/reference/react/useContext)
- [Redux Documentation](https://redux.js.org/)
- [Zustand Documentation](https://github.com/pmndrs/zustand)

## ➡️ Bước tiếp theo

Sau khi nắm vững State Management, hãy học [API Integration](../api-integration/)!

