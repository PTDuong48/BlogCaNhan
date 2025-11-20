---
title: "App đặt vé xe"
date: 2024-01-01
description: "Ứng dụng đặt vé xe khách với app Flutter và API ASP.NET Core. Hỗ trợ tìm kiếm, đặt vé, quản lý vé, check-in bằng QR, và chatbot AI"
image: "images/datve.png"
github: "#"
demo: "#"
tech_stack:
  frontend:
    - name: "Flutter"
      icon: "fab fa-flutter"
      color: "#02569b"
    - name: "Dart"
      icon: "fab fa-dart"
      color: "#0175c2"
    - name: "Provider"
      icon: "fas fa-box"
      color: "#6366f1"
    - name: "Go Router"
      icon: "fas fa-route"
      color: "#ca4245"
    - name: "Material Design"
      icon: "fab fa-google"
      color: "#4285f4"
    - name: "HTTP"
      icon: "fas fa-cloud"
      color: "#5a29e4"
    - name: "Shared Preferences"
      icon: "fas fa-save"
      color: "#10b981"
    - name: "QR Flutter"
      icon: "fas fa-qrcode"
      color: "#000000"
    - name: "Mobile Scanner"
      icon: "fas fa-camera"
      color: "#ff6b6b"
    - name: "Smart Auth"
      icon: "fas fa-fingerprint"
      color: "#f59e0b"
    - name: "Flutter SVG"
      icon: "fas fa-image"
      color: "#ec4899"
  backend:
    - name: "ASP.NET Core"
      icon: "fab fa-microsoft"
      color: "#512bd4"
    - name: "C#"
      icon: "fab fa-cuttlefish"
      color: "#239120"
    - name: "Entity Framework"
      icon: "fas fa-database"
      color: "#00a8e8"
    - name: "SQL Server"
      icon: "fas fa-server"
      color: "#cc2927"
    - name: "JWT"
      icon: "fas fa-key"
      color: "#d97706"
    - name: "ASP.NET Identity"
      icon: "fas fa-user-shield"
      color: "#512bd4"
    - name: "Swagger"
      icon: "fas fa-book"
      color: "#85ea2d"
  services:
    - name: "Google Gemini AI"
      icon: "fab fa-google"
      color: "#4285f4"
    - name: "ESMS"
      icon: "fas fa-sms"
      color: "#10b981"
    - name: "Google Maps"
      icon: "fas fa-map"
      color: "#4285f4"
---

## Tổng quan

Ứng dụng đặt vé xe khách với app Flutter và API ASP.NET Core. Hỗ trợ tìm kiếm, đặt vé, quản lý vé, check-in bằng QR, và chatbot AI.

## Kiến trúc hệ thống

- **Frontend**: Flutter (Android, iOS, Web)
- **Backend**: RESTful API (ASP.NET Core)
- **Database**: SQL Server với Entity Framework Core
- **Authentication**: JWT Bearer Token
- **State Management**: Provider pattern

## Tính năng chính

### 1. Quản lý người dùng

- Đăng ký/đăng nhập
- Xác thực OTP qua SMS
- Quên/đặt lại mật khẩu
- Xác thực sinh trắc học (vân tay/face ID)
- Phân quyền (Admin, Staff, Customer)

### 2. Tìm kiếm và đặt vé

- Tìm kiếm theo điểm đi, điểm đến, ngày
- Lọc theo giờ, giá, hãng xe
- Hiển thị danh sách chuyến với thông tin chi tiết
- Chọn ghế từ sơ đồ
- Đặt vé với thông tin hành khách
- Tạo mã QR điện tử sau khi đặt

### 3. Quản lý vé

- Xem danh sách vé đã đặt
- Chi tiết vé (thông tin chuyến, ghế, hành khách)
- Hủy vé (trong thời gian cho phép)
- Hiển thị mã QR để check-in

### 4. Check-in và quét QR

- Quét QR code từ vé
- Xác nhận thông tin và check-in
- Ghi log check-in
- Cập nhật trạng thái vé

### 5. Quản trị (Admin/Staff)

- Dashboard với thống kê
- Quản lý chuyến xe (CRUD)
- Quản lý tuyến đường
- Quản lý vé và theo dõi trạng thái
- Xem báo cáo và audit logs
- Quản lý người dùng

### 6. Chatbot AI

- Tích hợp Google Gemini AI
- Trả lời câu hỏi về đặt vé, chuyến xe, chính sách
- Hỗ trợ tiếng Việt

## Cấu trúc dữ liệu

### Models

- **User**: thông tin người dùng, roles
- **Route**: tuyến đường, điểm đi/đến
- **Trip**: chuyến xe, thời gian, giá, số ghế
- **Seat**: ghế, trạng thái
- **Booking**: vé, thông tin hành khách, QR code
- **CheckinLog**: lịch sử check-in
- **AuditLog**: lịch sử thao tác

## Bảo mật

- Mã hóa mật khẩu (ASP.NET Identity)
- JWT với expiration
- Token-based authentication
- QR code có token duy nhất
- Audit logging
- CORS
- Lockout sau nhiều lần đăng nhập sai

## Tích hợp dịch vụ bên ngoài

- **ESMS**: Gửi OTP qua SMS
- **Google Gemini AI**: Chatbot
- **Google Maps**: Mở bản đồ (URL launcher)

## Quy trình nghiệp vụ

### Đặt vé

1. Tìm kiếm chuyến
2. Chọn chuyến
3. Chọn ghế
4. Nhập thông tin hành khách
5. Xác nhận và thanh toán
6. Nhận mã QR

### Check-in

1. Nhân viên quét QR
2. Xác nhận thông tin
3. Check-in
4. Cập nhật trạng thái

## Tối ưu và trải nghiệm

- Material Design 3
- Loading indicators
- Form validation
- Xử lý lỗi
- Responsive design
- Lưu trữ local (SharedPreferences)
- Cấu hình API linh hoạt

## Môi trường phát triển

- Hỗ trợ Android, iOS, Web
- Swagger UI cho API testing
- Database migrations tự động
- Cấu hình môi trường (Development/Production)

Dự án áp dụng các công nghệ hiện đại, kiến trúc rõ ràng, và tập trung vào bảo mật và trải nghiệm người dùng.

