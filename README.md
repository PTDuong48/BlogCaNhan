# Blog Lập Trình Mạng - Java & JavaScript

Website blog cá nhân chuyên về lập trình mạng với Java và JavaScript, được xây dựng bằng Hugo Static Site Generator.

## 🚀 Tính Năng

- ✅ **Trang chủ** với giới thiệu và bài viết nổi bật
- ✅ **Trang Blog** với 9+ bài viết về Java & JavaScript
- ✅ **Trang About Me** với thông tin chi tiết về tác giả
- ✅ **Trang Certificates** hiển thị các chứng chỉ Cisco
- ✅ **Responsive Design** - Tối ưu cho mọi thiết bị
- ✅ **SEO Optimized** - Tối ưu cho công cụ tìm kiếm
- ✅ **Code Highlighting** - Hỗ trợ highlight code Java & JavaScript
- ✅ **Modern UI** - Giao diện hiện đại, đẹp mắt

## 📋 Yêu Cầu

- [Hugo](https://gohugo.io/) (phiên bản 0.100.0 trở lên)
- Git
- GitHub account (để deploy)

## 🛠️ Cài Đặt

### 1. Clone Repository

```bash
git clone https://github.com/yourusername/BlogCaNhan.git
cd BlogCaNhan
```

### 2. Cài Đặt Hugo

#### Windows

**Cách 1: Tải trực tiếp (Khuyến nghị)**

1. Truy cập [Hugo Releases](https://github.com/gohugoio/hugo/releases)
2. Tải file `hugo_extended_X.X.X_windows-amd64.zip` (phiên bản mới nhất)
3. Giải nén file zip
4. Tạo thư mục `C:\Hugo\bin` (hoặc thư mục khác bạn muốn)
5. Copy file `hugo.exe` vào thư mục đó
6. Thêm `C:\Hugo\bin` vào biến môi trường PATH:
   - Mở "Environment Variables" trong Windows Settings
   - Tìm "Path" trong System variables
   - Click "Edit" → "New" → Thêm `C:\Hugo\bin`
   - Click "OK" để lưu
7. Mở lại terminal và kiểm tra: `hugo version`

**Cách 2: Với Chocolatey (nếu đã cài)**

```bash
choco install hugo-extended
```

**Cách 3: Với Scoop (nếu đã cài)**

```bash
scoop install hugo-extended
```

#### macOS

```bash
brew install hugo
```

#### Linux

```bash
sudo apt-get install hugo
```

**Lưu ý:** Trên Windows, bạn KHÔNG thể dùng `sudo apt-get` vì đó là lệnh Linux. Hãy dùng một trong các cách trên.

### 3. Chạy Local Server

```bash
hugo server
```

Website sẽ chạy tại: `http://localhost:1313`

## 📁 Cấu Trúc Thư Mục

```
BlogCaNhan/
├── config.toml              # Cấu hình Hugo
├── content/                  # Nội dung website
│   ├── posts/               # Các bài viết blog
│   ├── about/               # Trang About Me
│   └── certificates/        # Trang Certificates
├── themes/
│   └── custom-theme/        # Theme tùy chỉnh
│       ├── layouts/         # Templates
│       ├── static/          # CSS, JS, images
│       │   ├── css/
│       │   └── js/
└── README.md
```

## ✍️ Thêm Bài Viết Mới

Tạo file markdown mới trong thư mục `content/posts/`:

```bash
hugo new posts/ten-bai-viet.md
```

Front matter mẫu:

```yaml
---
title: "Tiêu Đề Bài Viết"
date: 2025-01-20
category: "java" # hoặc "javascript", "network"
tags: ["Java", "Network", "Socket"]
summary: "Tóm tắt ngắn gọn về nội dung bài viết"
---
```

## 🎨 Tùy Chỉnh

### Thay Đổi Thông Tin Cá Nhân

1. **config.toml**: Sửa `title`, `params.author`, `params.description`
2. **content/about/\_index.md**: Sửa thông tin về bản thân
3. **content/certificates/\_index.md**: Thêm/sửa chứng chỉ

### Thay Đổi Màu Sắc

Sửa file `themes/custom-theme/static/css/style.css`:

```css
:root {
  --primary: #2563eb; /* Màu chính */
  --secondary: #10b981; /* Màu phụ */
  --dark: #1e293b; /* Màu chữ */
  /* ... */
}
```

## 🚀 Deploy Lên GitHub Pages

### Cách 1: Sử dụng GitHub Actions (Khuyến nghị)

1. **Tạo repository trên GitHub**

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/BlogCaNhan.git
git push -u origin main
```

2. **Tạo GitHub Actions Workflow**

Tạo file `.github/workflows/gh-pages.yml`:

```yaml
name: Deploy Hugo Site

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest"
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

3. **Cấu hình GitHub Pages**

- Vào Settings → Pages
- Source: Deploy from a branch
- Branch: `gh-pages` / `/(root)`

4. **Cập nhật baseURL trong config.toml**

```toml
baseURL = "https://yourusername.github.io/BlogCaNhan/"
```

### Cách 2: Deploy Thủ Công

```bash
# Build static site
hugo

# Clone gh-pages branch
git clone -b gh-pages https://github.com/yourusername/BlogCaNhan.git public-temp

# Copy files
cp -r public/* public-temp/

# Commit và push
cd public-temp
git add .
git commit -m "Update site"
git push origin gh-pages
```

## 📝 Nội Dung Website

### Bài Viết Blog (9 bài)

1. Giới Thiệu Java và Môi Trường Lập Trình
2. Các Vòng Lặp Trong JavaScript
3. Xử Lý Mạng Cơ Bản Trong Java
4. Event Loop Trong JavaScript
5. Hướng Dẫn Kết Nối MySQL Với Java
6. DOM Manipulation Trong JavaScript
7. Lập Trình Socket Java Cơ Bản
8. Async/Await Trong JavaScript
9. Debugging Trong Java & JavaScript

### Trang Certificates

Hiển thị 6 chứng chỉ Cisco mẫu:

- CCNA
- CCNP Enterprise
- CCNA Security
- DevNet Associate
- Enterprise Core
- Enterprise Advanced Infrastructure

## 🔧 Troubleshooting

### Lỗi: "command not found: hugo"

Cài đặt Hugo và đảm bảo nó có trong PATH.

### Lỗi: Theme không tìm thấy

Kiểm tra `config.toml` có đúng tên theme: `theme = "custom-theme"`

### Lỗi khi build

```bash
# Xóa cache và build lại
rm -rf public resources
hugo --cleanDestinationDir
```

## 📚 Tài Liệu Tham Khảo

- [Hugo Documentation](https://gohugo.io/documentation/)
- [Hugo Themes](https://themes.gohugo.io/)
- [GitHub Pages](https://pages.github.com/)

## 📄 License

MIT License - Tự do sử dụng và chỉnh sửa.

## 👤 Tác Giả

**Network Developer**

- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your Profile](https://linkedin.com/in/yourprofile)
- Email: contact@example.com

## 🙏 Cảm Ơn

Cảm ơn bạn đã quan tâm đến blog này! Nếu có câu hỏi hoặc góp ý, vui lòng tạo issue trên GitHub.

---

⭐ Nếu bạn thấy project này hữu ích, hãy cho một star nhé!
