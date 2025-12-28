---
title: "Build Tools"
date: 2025-01-20
description: "Webpack, Vite và các công cụ build hiện đại"
weight: 11
---

# Build Tools

Build Tools giúp bạn biên dịch, tối ưu và bundle code để deploy lên production. Chúng là phần quan trọng trong workflow phát triển hiện đại.

## 🛠️ Build Tools là gì?

Build Tools xử lý:
- Transpiling (Babel, TypeScript)
- Bundling (kết hợp nhiều file thành một)
- Minification (nén code)
- Code splitting
- Hot Module Replacement (HMR)

## 🎬 Video hướng dẫn

<!-- Chưa có video cho phần này -->

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/BuildTools.jpg" alt="Build Tools" />

## 📚 Các công cụ phổ biến

### 1. Webpack

Webpack là module bundler phổ biến nhất:

```javascript
// webpack.config.js
module.exports = {
    entry: './src/index.js',
    output: {
        path: __dirname + '/dist',
        filename: 'bundle.js'
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                use: 'babel-loader'
            },
            {
                test: /\.css$/,
                use: ['style-loader', 'css-loader']
            }
        ]
    }
};
```

### 2. Vite

Vite là build tool mới, nhanh hơn Webpack:

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
    plugins: [react()],
    server: {
        port: 3000
    }
});
```

### 3. Create React App

```bash
npx create-react-app my-app
cd my-app
npm start
```

### 4. Next.js

Next.js là React framework với build tools tích hợp:

```bash
npx create-next-app@latest my-app
```

## 📖 Nội dung cần học

- Webpack configuration
- Vite setup
- Babel và transpiling
- CSS preprocessing (Sass, Less)
- Environment variables
- Code splitting
- Performance optimization

## 📊 So sánh

| Tool | Tốc độ | Độ phức tạp | Phù hợp cho |
|------|--------|-------------|-------------|
| **Webpack** | Trung bình | Cao | Dự án lớn, cần customization |
| **Vite** | Rất nhanh | Thấp | Dự án mới, cần tốc độ |
| **CRA** | Nhanh | Thấp | Dự án React đơn giản |
| **Next.js** | Nhanh | Trung bình | Full-stack React apps |

## ✅ Best Practices

- Sử dụng code splitting để tối ưu
- Minify và compress assets
- Sử dụng environment variables
- Tối ưu bundle size
- Cache busting cho production

## 💪 Thực hành

1. Setup Webpack cho project
2. Migrate sang Vite
3. Tối ưu build performance
4. Setup production build

## 🔗 Tài nguyên

- [Webpack Documentation](https://webpack.js.org/)
- [Vite Documentation](https://vitejs.dev/)
- [Next.js Documentation](https://nextjs.org/docs)

## ➡️ Bước tiếp theo

Sau khi nắm vững Build Tools, hãy học [Testing](../testing/)!

