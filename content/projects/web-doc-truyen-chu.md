---
title: "Web đọc truyện chữ"
date: 2024-01-01
description: "Nền tảng đọc truyện trực tuyến với hệ thống quản lý nội dung, thanh toán bằng xu, và phân quyền người dùng"
image: "images/truyen.png"
github: "https://github.com/PTDuong48"
demo: "https://youtu.be/Bt7cRFGBQ34"
tech_stack:
  backend:
    - name: "Node.js"
      icon: "fab fa-node-js"
      color: "#22c55e"
    - name: "Express.js"
      icon: "fas fa-server"
      color: "#000000"
    - name: "MongoDB"
      icon: "fas fa-database"
      color: "#47a248"
    - name: "Mongoose"
      icon: "fas fa-leaf"
      color: "#880000"
    - name: "JWT"
      icon: "fas fa-key"
      color: "#d97706"
    - name: "Bcrypt"
      icon: "fas fa-lock"
      color: "#dc2626"
    - name: "Multer"
      icon: "fas fa-upload"
      color: "#7c3aed"
    - name: "Nodemailer"
      icon: "fas fa-envelope"
      color: "#ea580c"
  frontend:
    - name: "HTML5"
      icon: "fab fa-html5"
      color: "#f97316"
    - name: "CSS3"
      icon: "fab fa-css3-alt"
      color: "#3b82f6"
    - name: "JavaScript"
      icon: "fab fa-js"
      color: "#eab308"
    - name: "EJS"
      icon: "fas fa-code"
      color: "#a855f7"
    - name: "jQuery"
      icon: "fab fa-js-square"
      color: "#0769ad"
    - name: "Bootstrap"
      icon: "fab fa-bootstrap"
      color: "#7952b3"
    - name: "Font Awesome"
      icon: "fab fa-font-awesome"
      color: "#528dd7"
  tools:
    - name: "Nodemon"
      icon: "fas fa-sync"
      color: "#10b981"
    - name: "Dotenv"
      icon: "fas fa-cog"
      color: "#6366f1"
---

## Tổng quan

Nền tảng đọc truyện trực tuyến với hệ thống quản lý nội dung, thanh toán bằng xu, và phân quyền người dùng. Hỗ trợ đọc truyện miễn phí và VIP, quản lý tác giả, và hệ thống thanh toán tích hợp.

## Tính năng chính

### 1. Hệ thống người dùng

- Đăng ký/đăng nhập với xác thực email
- Phân quyền: Độc giả, Tác giả, Quản trị viên
- Quản lý hồ sơ: avatar, thông tin cá nhân
- Theo dõi truyện: danh sách truyện đang theo dõi, cập nhật chương mới
- Lịch sử đọc: lưu vị trí đọc, danh sách truyện đã đọc
- Đánh giá truyện: rating và bình luận
- Quản lý xu: số dư, lịch sử giao dịch

### 2. Hệ thống đọc truyện

- Danh sách truyện: hiển thị theo thể loại, trạng thái, độ hot/featured
- Tìm kiếm và lọc: theo tiêu đề, tác giả, thể loại, trạng thái
- Chi tiết truyện: mô tả, thể loại, rating, số chương, trạng thái
- Đọc chương: giao diện đọc, điều hướng chương, đánh dấu đã đọc
- Chương VIP: mua bằng xu, kiểm tra quyền truy cập
- Bình luận: bình luận và phản hồi, like, xóa

### 3. Hệ thống thanh toán

- Nạp xu: nhiều gói xu (100, 300, 500, 1000, 2000, 5000)
- Phương thức thanh toán:
  - VNPAY: thẻ ATM, Visa/MasterCard, QR Code
  - Chuyển khoản ngân hàng: hỗ trợ nhiều ngân hàng
- Giao dịch: tạo, theo dõi, duyệt/hủy (admin)
- Lịch sử giao dịch: chi tiết nạp và sử dụng xu

### 4. Quản lý nội dung (Tác giả)

- Tạo và quản lý truyện: thông tin, ảnh bìa, thể loại, mô tả
- Quản lý chương: thêm, sửa, xóa, đặt giá xu (chương VIP)
- Duyệt nội dung: gửi chương để admin duyệt trước khi xuất bản
- Thống kê: lượt xem, rating, bình luận

### 5. Bảng điều khiển quản trị viên

- Dashboard: thống kê tổng quan (số người dùng, truyện, chương, giao dịch)
- Quản lý truyện: CRUD, duyệt, gán featured/hot
- Quản lý chương: duyệt/từ chối, chỉnh sửa, xóa
- Quản lý người dùng: danh sách, khóa/mở khóa, phân quyền
- Quản lý giao dịch: duyệt/hủy, xem chi tiết, thống kê doanh thu
- Quản lý thể loại: thêm, sửa, xóa
- Quản lý gói xu: tạo, chỉnh sửa, xóa gói nạp xu
- Cài đặt hệ thống: cấu hình chung

## Kiến trúc hệ thống

### Backend Architecture

- Mô hình MVC: tách routes, controllers, models
- Middleware: xác thực, phân quyền, xử lý lỗi
- RESTful API: endpoints chuẩn
- Session-based authentication: quản lý phiên đăng nhập

### Database Schema

- User: thông tin người dùng, xu, lịch sử đọc, truyện theo dõi
- Story: thông tin truyện, thể loại, rating, lượt xem
- Chapter: nội dung chương, giá xu, trạng thái duyệt
- Transaction: giao dịch nạp/sử dụng xu
- CoinPackage: gói nạp xu
- Comment: bình luận, phản hồi, like
- Genre: thể loại truyện
- Rating: đánh giá truyện
- PaymentHistory: lịch sử thanh toán

### Frontend Architecture

- Single Page Application: điều hướng bằng JavaScript
- Module-based JavaScript: tách chức năng theo module
- AJAX: tương tác không đồng bộ với API
- Responsive Design: hỗ trợ nhiều thiết bị

## Bảo mật

- Mã hóa mật khẩu bằng bcrypt
- JWT cho xác thực API
- Session management
- Phân quyền theo role
- Validation dữ liệu đầu vào
- CORS

## Tính năng bổ sung

- Upload ảnh: avatar, ảnh bìa truyện
- Email verification: xác thực email khi đăng ký
- Password reset: đặt lại mật khẩu qua email
- View tracking: đếm lượt xem truyện/chương
- Reading progress: lưu tiến độ đọc
- Related stories: gợi ý truyện liên quan
