---
title: "Git & Version Control"
date: 2025-01-20
description: "Quản lý mã nguồn với Git và GitHub"
weight: 7
---

# Git & Version Control

Git là hệ thống quản lý phiên bản phân tán, giúp bạn theo dõi thay đổi trong code và cộng tác với team.

## 📦 Git là gì?

Git là công cụ quản lý phiên bản mã nguồn, cho phép bạn:
- Theo dõi lịch sử thay đổi
- Làm việc nhóm hiệu quả
- Quay lại phiên bản cũ
- Tạo nhánh (branch) để phát triển tính năng mới

## 🎬 Video hướng dẫn

<div class="video-container">
  <iframe 
    width="100%" 
    height="450" 
    src="https://www.youtube.com/embed/e9lnsKot_SQ" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
    allowfullscreen>
  </iframe>
</div>

## 🖼️ Hình ảnh minh họa

<img src="/BlogCaNhan/images/roadmap/Git-VersionControl.jpg" alt="Git & Version Control" />

## 💻 Các lệnh Git cơ bản

### Khởi tạo và cấu hình

```bash
# Cài đặt Git (đã có sẵn trên hầu hết hệ thống)
git --version

# Cấu hình
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Các lệnh cơ bản

```bash
# Khởi tạo repository
git init

# Kiểm tra trạng thái
git status

# Thêm file vào staging
git add .
git add filename.js

# Commit
git commit -m "Initial commit"

# Xem lịch sử
git log

# Tạo branch
git branch feature-name
git checkout feature-name

# Merge branch
git merge feature-name

# Clone repository
git clone https://github.com/username/repo.git

# Push lên remote
git push origin main

# Pull từ remote
git pull origin main
```

## 🌐 GitHub

GitHub là nền tảng lưu trữ code sử dụng Git, cung cấp:
- Lưu trữ code miễn phí
- Collaboration tools
- Issue tracking
- Pull requests
- GitHub Pages (hosting)

## 🔄 Workflow cơ bản

1. **Clone** repository từ GitHub
2. **Tạo branch** mới cho feature
3. **Code** và **commit** thay đổi
4. **Push** lên GitHub
5. **Tạo Pull Request** để merge vào main
6. **Review** và **merge**

## ✅ Best Practices

- Commit thường xuyên với message rõ ràng
- Sử dụng .gitignore để loại trừ file không cần thiết
- Tạo branch cho mỗi feature mới
- Không commit code lỗi vào main branch

## 💪 Thực hành

1. Tạo GitHub account
2. Tạo repository mới
3. Clone và push code
4. Tạo branch và merge
5. Sử dụng GitHub Pages để deploy

## 🔗 Tài nguyên

- [Git Documentation](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [Learn Git Branching](https://learngitbranching.js.org/)

## ➡️ Bước tiếp theo

Sau khi nắm vững Git, hãy học [React.js](../reactjs/)!

