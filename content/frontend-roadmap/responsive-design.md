---
title: "Responsive Design"
date: 2025-01-20
description: "Tạo website hiển thị tốt trên mọi thiết bị"
weight: 4
---

# Responsive Design

Responsive Design là kỹ thuật thiết kế website để tự động điều chỉnh và hiển thị tốt trên mọi kích thước màn hình, từ điện thoại đến máy tính bảng và desktop.

## 📱 Responsive Design là gì?

Responsive Design đảm bảo rằng website của bạn trông đẹp và hoạt động tốt trên:
- Điện thoại di động (320px - 768px)
- Máy tính bảng (768px - 1024px)
- Desktop (1024px trở lên)

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/l04dDYW-QaI" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/ResponsiveDesign.jpg" alt="Responsive Design" />

## 📚 Nội dung cần học

### Media Queries

```css
/* Mobile First Approach */
.container {
    width: 100%;
    padding: 10px;
}

/* Tablet */
@media (min-width: 768px) {
    .container {
        width: 750px;
        margin: 0 auto;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    .container {
        width: 1200px;
    }
}
```

### Viewport Meta Tag

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Flexible Units

- Percentage (%)
- Viewport units (vw, vh)
- rem và em
- max-width và min-width

### Flexible Images

```css
img {
    max-width: 100%;
    height: auto;
}
```

### Flexbox và Grid

- Flexbox cho layout 1 chiều
- CSS Grid cho layout 2 chiều
- Responsive với flexbox và grid

## ✅ Best Practices

1. **Mobile First**: Thiết kế cho mobile trước
2. **Breakpoints**: Sử dụng breakpoints hợp lý
3. **Touch-friendly**: Buttons và links đủ lớn để click
4. **Performance**: Tối ưu ảnh và code
5. **Testing**: Test trên nhiều thiết bị

## 💪 Thực hành

1. Tạo responsive navigation menu
2. Xây dựng responsive card layout
3. Tạo responsive form
4. Build responsive landing page

## 🔗 Tài nguyên

- [MDN Responsive Design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
- [CSS-Tricks Responsive Design](https://css-tricks.com/snippets/css/complete-guide-grid/)

## ➡️ Bước tiếp theo

Sau khi nắm vững Responsive Design, hãy học [CSS Framework](../css-framework/)!

