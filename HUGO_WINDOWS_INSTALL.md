# Hướng Dẫn Cài Đặt Hugo Trên Windows

## Phương Pháp 1: Tải Trực Tiếp (Khuyến nghị)

### Bước 1: Tải Hugo

1. Truy cập: https://github.com/gohugoio/hugo/releases
2. Tìm phiên bản mới nhất (ví dụ: `hugo_extended_0.121.0_windows-amd64.zip`)
3. Tải file `.zip` về máy

### Bước 2: Giải Nén

1. Giải nén file zip vừa tải
2. Bạn sẽ thấy file `hugo.exe`

### Bước 3: Tạo Thư Mục và Copy File

1. Tạo thư mục: `C:\Hugo\bin` (hoặc bất kỳ thư mục nào bạn muốn)
2. Copy file `hugo.exe` vào thư mục đó

### Bước 4: Thêm Vào PATH

**Cách 1: Qua Settings (Windows 10/11)**

1. Mở **Settings** → **System** → **About**
2. Click **Advanced system settings**
3. Click **Environment Variables**
4. Trong **System variables**, tìm và chọn **Path**
5. Click **Edit**
6. Click **New**
7. Thêm đường dẫn: `C:\Hugo\bin`
8. Click **OK** để lưu tất cả

**Cách 2: Qua Command Prompt (Admin)**

```cmd
setx PATH "%PATH%;C:\Hugo\bin" /M
```

### Bước 5: Kiểm Tra

1. **Đóng tất cả terminal/command prompt hiện tại**
2. Mở terminal mới
3. Chạy lệnh:

```bash
hugo version
```

Nếu thấy version number, bạn đã cài đặt thành công!

---

## Phương Pháp 2: Chocolatey

### Yêu Cầu

- Đã cài Chocolatey: https://chocolatey.org/install

### Cài Đặt

Mở PowerShell (Run as Administrator):

```powershell
choco install hugo-extended -y
```

### Kiểm Tra

```bash
hugo version
```

---

## Phương Pháp 3: Scoop

### Yêu Cầu

- Đã cài Scoop: https://scoop.sh/

### Cài Đặt

```bash
scoop install hugo-extended
```

### Kiểm Tra

```bash
hugo version
```

---

## Troubleshooting

### Lỗi: "hugo: command not found"

- Đảm bảo đã thêm Hugo vào PATH
- **Đóng và mở lại terminal** sau khi thêm PATH
- Kiểm tra đường dẫn: `echo %PATH%` (Windows) hoặc `echo $PATH` (Git Bash)

### Lỗi: "hugo: permission denied"

- Chạy terminal với quyền Administrator
- Hoặc di chuyển Hugo vào thư mục không cần quyền admin

### Kiểm Tra Đường Dẫn

```bash
where hugo
```

Lệnh này sẽ hiển thị đường dẫn đến file hugo.exe

---

## Sau Khi Cài Đặt

Bạn có thể chạy website bằng:

```bash
cd BlogCaNhan
hugo server
```

Website sẽ chạy tại: http://localhost:1313
