# Hướng dẫn thêm ảnh và video YouTube vào trang Lộ trình Frontend

## Cách thêm Video YouTube

### Bước 1: Lấy Video ID từ YouTube

1. Mở video YouTube bạn muốn thêm
2. Copy URL của video (ví dụ: `https://www.youtube.com/watch?v=dQw4w9WgXcQ`)
3. Video ID là phần sau `v=` (trong ví dụ trên là `dQw4w9WgXcQ`)

### Bước 2: Thêm video vào file Markdown

Tìm dòng có comment `<!-- PLACEHOLDER VIDEO YOUTUBE -->` trong file markdown và thay thế bằng:

```html
<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/VIDEO_ID" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>
```

**Ví dụ:**
```html
<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>
```

### Lưu ý:
- Thay `VIDEO_ID` bằng ID thực tế của video
- Video sẽ tự động responsive trên mọi thiết bị

---

## Cách thêm Ảnh

### Bước 1: Thêm ảnh vào thư mục

1. Tạo thư mục `themes/custom-theme/static/images/roadmap/` (nếu chưa có)
2. Copy ảnh vào thư mục này
3. Đặt tên file dễ nhớ (ví dụ: `html-css-overview.jpg`)

### Bước 2: Thêm ảnh vào file Markdown

Tìm dòng có comment `<!-- PLACEHOLDER IMAGE -->` và thay thế bằng:

```markdown
![Mô tả ảnh](/images/roadmap/ten-file-anh.jpg)
```

**Ví dụ:**
```markdown
![HTML và CSS cơ bản - Tổng quan](/images/roadmap/html-css-overview.jpg)
```

### Hoặc sử dụng HTML để có thêm control:

```html
<div class="image-container">
  <img 
    src="/images/roadmap/ten-file-anh.jpg" 
    alt="Mô tả ảnh" 
    class="roadmap-image"
  />
  <p class="image-caption">Chú thích ảnh (tùy chọn)</p>
</div>
```

### Lưu ý:
- Đường dẫn bắt đầu từ `/images/` (không cần `themes/custom-theme/static/`)
- Nên sử dụng định dạng `.jpg`, `.png`, hoặc `.webp`
- Tối ưu kích thước ảnh trước khi upload (khuyến nghị < 500KB)
- Đặt tên file không có dấu và khoảng trắng (dùng dấu gạch ngang `-`)

---

## Ví dụ hoàn chỉnh

### Trước (Placeholder):
```html
<!-- PLACEHOLDER VIDEO YOUTUBE -->
<div class="video-placeholder">
  <h3>Video: Học HTML & CSS từ đầu</h3>
  <p>Thêm video YouTube tại đây</p>
</div>

<!-- PLACEHOLDER IMAGE -->
<div class="image-placeholder">
  <h3>Ảnh: HTML Structure</h3>
  <p>Thêm ảnh minh họa cấu trúc HTML tại đây</p>
</div>
```

### Sau (Đã thêm nội dung):
```html
<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/UB1O30fR-EE" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

![Cấu trúc HTML cơ bản](/images/roadmap/html-structure.jpg)
```

---

## Các file cần chỉnh sửa

Các file markdown trong thư mục `content/frontend-roadmap/`:

1. `_index.md` - Trang tổng quan
2. `html-css-basics.md` - HTML & CSS cơ bản
3. `javascript-basics.md` - JavaScript cơ bản
4. `responsive-design.md` - Responsive Design
5. `css-framework.md` - CSS Framework
6. `javascript-es6.md` - JavaScript ES6+
7. `git-version-control.md` - Git & Version Control
8. `reactjs.md` - React.js
9. `state-management.md` - State Management
10. `api-integration.md` - API Integration
11. `build-tools.md` - Build Tools
12. `testing.md` - Testing
13. `deployment.md` - Deployment

---

## Tips

1. **Video YouTube:**
   - Chọn video chất lượng tốt, có phụ đề tiếng Việt nếu có thể
   - Video nên có độ dài phù hợp (10-30 phút cho tutorial)
   - Kiểm tra video có bị chặn ở một số quốc gia không

2. **Ảnh:**
   - Sử dụng ảnh minh họa rõ ràng, dễ hiểu
   - Có thể dùng screenshot từ code editor
   - Hoặc tìm ảnh miễn phí trên Unsplash, Pexels
   - Nên có kích thước nhất quán (ví dụ: 1200x600px)

3. **Tối ưu:**
   - Nén ảnh trước khi upload để tăng tốc độ tải trang
   - Sử dụng format WebP cho ảnh nếu có thể
   - Kiểm tra hiển thị trên mobile sau khi thêm

---

## Cần hỗ trợ?

Nếu gặp vấn đề khi thêm ảnh/video, hãy kiểm tra:
1. Đường dẫn file có đúng không
2. File ảnh có tồn tại trong thư mục không
3. Video ID có đúng không
4. Đã build lại Hugo chưa (`hugo server`)

