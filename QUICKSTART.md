# Hướng Dẫn Nhanh

## Bước 1: Cài Đặt Hugo

### Windows
```bash
# Với Chocolatey
choco install hugo-extended

# Hoặc tải từ: https://github.com/gohugoio/hugo/releases
```

### macOS
```bash
brew install hugo
```

### Linux
```bash
sudo apt-get install hugo
```

## Bước 2: Chạy Website

```bash
# Di chuyển vào thư mục project
cd BlogCaNhan

# Chạy server development
hugo server

# Website sẽ chạy tại: http://localhost:1313
```

## Bước 3: Build Static Site

```bash
# Build website
hugo

# Files sẽ được tạo trong thư mục /public
```

## Bước 4: Deploy Lên GitHub

1. Tạo repository trên GitHub
2. Push code lên GitHub
3. GitHub Actions sẽ tự động build và deploy

Chi tiết xem trong [README.md](README.md)

## Cấu Trúc Quan Trọng

- `content/posts/` - Các bài viết blog
- `content/about/_index.md` - Trang About Me
- `content/certificates/_index.md` - Trang Certificates
- `themes/custom-theme/` - Theme tùy chỉnh
- `config.toml` - Cấu hình Hugo

## Thêm Bài Viết Mới

```bash
hugo new posts/ten-bai-viet.md
```

Sau đó chỉnh sửa file markdown trong `content/posts/`

## Tùy Chỉnh

- **Thông tin cá nhân:** Sửa `content/about/_index.md`
- **Chứng chỉ:** Sửa `content/certificates/_index.md`
- **Màu sắc:** Sửa `themes/custom-theme/static/css/style.css`
- **Cấu hình:** Sửa `config.toml`

## Troubleshooting

Nếu gặp lỗi, thử:

```bash
# Xóa cache
rm -rf public resources

# Build lại
hugo --cleanDestinationDir
```

