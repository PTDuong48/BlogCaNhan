---
title: "Deployment"
date: 2025-01-20
description: "Triển khai ứng dụng Frontend lên production"
weight: 13
---

# Deployment

Deployment là quá trình đưa ứng dụng lên môi trường production để người dùng có thể truy cập. Đây là bước cuối cùng trong quy trình phát triển.

## 🚀 Deployment là gì?

Deployment bao gồm:
- Build ứng dụng cho production
- Upload lên hosting service
- Cấu hình domain và SSL
- Setup CI/CD pipeline

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/nZ3BaTY8c9M?start=31" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/Deployment.jpg" alt="Deployment" />

## 📚 Các nền tảng deployment

### 1. Vercel

Tốt nhất cho React và Next.js:

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

### 2. Netlify

Dễ sử dụng, hỗ trợ nhiều framework:

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Deploy
netlify deploy --prod
```

### 3. GitHub Pages

Miễn phí cho static sites:

```bash
# Build
npm run build

# Deploy với gh-pages
npm install --save-dev gh-pages
```

### 4. AWS S3 + CloudFront

Cho ứng dụng lớn, cần performance cao:

```bash
# Build
npm run build

# Upload to S3
aws s3 sync build/ s3://your-bucket-name
```

## 🔨 Build cho Production

```bash
# React
npm run build

# Next.js
npm run build
npm start

# Vite
npm run build
```

## 🔐 Environment Variables

```bash
# .env.production
REACT_APP_API_URL=https://api.production.com
REACT_APP_API_KEY=your-api-key
```

## ⚙️ CI/CD với GitHub Actions

```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    branches: [ main ]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
      - run: npm install
      - run: npm run build
      - run: npm run deploy
```

## ✅ Best Practices

- Minify và compress assets
- Enable gzip compression
- Setup CDN cho static assets
- Configure caching headers
- Use HTTPS
- Monitor performance
- Setup error tracking (Sentry)

## 💪 Thực hành

1. Deploy React app lên Vercel
2. Setup custom domain
3. Configure CI/CD pipeline
4. Monitor và optimize performance

## 🔗 Tài nguyên

- [Vercel Documentation](https://vercel.com/docs)
- [Netlify Documentation](https://docs.netlify.com/)
- [GitHub Pages](https://pages.github.com/)

## 🎉 Kết thúc lộ trình

Chúc mừng! Bạn đã hoàn thành lộ trình Frontend Developer. Tiếp tục thực hành và xây dựng các dự án thực tế để củng cố kiến thức!

