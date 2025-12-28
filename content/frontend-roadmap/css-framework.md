---
title: "CSS Framework"
date: 2025-01-20
description: "Sử dụng Bootstrap và Tailwind CSS để phát triển nhanh hơn"
weight: 5
---

# CSS Framework

CSS Framework giúp bạn phát triển giao diện nhanh hơn bằng cách cung cấp các component và utility classes có sẵn.

## 🎨 CSS Framework là gì?

CSS Framework là bộ thư viện CSS được thiết kế sẵn với các component, grid system, và utility classes giúp bạn xây dựng website nhanh chóng và nhất quán.

### Framework phổ biến

- **Bootstrap**: Framework phổ biến nhất, dễ học
- **Tailwind CSS**: Utility-first CSS framework
- **Material-UI**: Dựa trên Material Design
- **Bulma**: Framework hiện đại, không cần JavaScript

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/MyCvTSjkD74" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/CSSFramework.jpg" alt="CSS Framework" />

## 🅱️ Bootstrap

### Cài đặt

```html
<!-- Bootstrap CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<!-- Bootstrap JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

### Ví dụ sử dụng

```html
<div class="container">
    <div class="row">
        <div class="col-md-6">
            <div class="card">
                <div class="card-body">
                    <h5 class="card-title">Card Title</h5>
                    <p class="card-text">Card content</p>
                </div>
            </div>
        </div>
    </div>
</div>
```

## 💨 Tailwind CSS

### Cài đặt

```html
<script src="https://cdn.tailwindcss.com"></script>
```

### Ví dụ sử dụng

```html
<div class="container mx-auto px-4">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        <div class="bg-white rounded-lg shadow p-6">
            <h3 class="text-xl font-bold mb-2">Card Title</h3>
            <p class="text-gray-600">Card content</p>
        </div>
    </div>
</div>
```

## 📚 Nội dung cần học

### Bootstrap

- Grid system
- Components (buttons, cards, forms, navbar)
- Utilities
- Customization

### Tailwind CSS

- Utility classes
- Responsive design
- Custom configuration
- Plugins

## 💡 Khi nào dùng gì?

- **Bootstrap**: Dự án cần component có sẵn, team lớn
- **Tailwind**: Dự án cần customization cao, design độc đáo

## 💪 Thực hành

1. Xây dựng landing page với Bootstrap
2. Tạo dashboard với Tailwind CSS
3. So sánh và chọn framework phù hợp

## 🔗 Tài nguyên

- [Bootstrap Documentation](https://getbootstrap.com/docs/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)

## ➡️ Bước tiếp theo

Sau khi nắm vững CSS Framework, hãy học [JavaScript ES6+](../javascript-es6/)!

