---
title: "StudyQ&A"
date: 2024-01-01
description: "Hệ thống hỏi đáp dựa trên tài liệu, sử dụng RAG (Retrieval-Augmented Generation) và AI để trả lời câu hỏi từ nội dung tài liệu"
image: "images/study.png"
github: "https://github.com/PTDuong48/StudyQ-A_RAG.git"
demo: "https://youtu.be/imVoehncGPI"
tech_stack:
  backend:
    - name: "FastAPI"
      icon: "fas fa-bolt"
      color: "#009688"
    - name: "Uvicorn"
      icon: "fas fa-server"
      color: "#4caf50"
    - name: "MongoDB"
      icon: "fas fa-database"
      color: "#47a248"
    - name: "Motor"
      icon: "fas fa-cog"
      color: "#00bcd4"
    - name: "FAISS"
      icon: "fas fa-search"
      color: "#ff9800"
    - name: "OpenAI"
      icon: "fas fa-brain"
      color: "#10a37f"
    - name: "Gemini"
      icon: "fab fa-google"
      color: "#4285f4"
    - name: "LangChain"
      icon: "fas fa-link"
      color: "#00a67e"
    - name: "PyMuPDF"
      icon: "fas fa-file-pdf"
      color: "#f40f02"
    - name: "python-docx"
      icon: "fas fa-file-word"
      color: "#2b579a"
    - name: "JWT"
      icon: "fas fa-key"
      color: "#d97706"
    - name: "Bcrypt"
      icon: "fas fa-lock"
      color: "#dc2626"
    - name: "Cryptography"
      icon: "fas fa-shield-alt"
      color: "#6366f1"
  frontend:
    - name: "React"
      icon: "fab fa-react"
      color: "#61dafb"
    - name: "React Router"
      icon: "fas fa-route"
      color: "#ca4245"
    - name: "Vite"
      icon: "fas fa-bolt"
      color: "#646cff"
    - name: "Axios"
      icon: "fas fa-cloud"
      color: "#5a29e4"
    - name: "Tailwind CSS"
      icon: "fas fa-wind"
      color: "#06b6d4"
    - name: "React Markdown"
      icon: "fas fa-markdown"
      color: "#083fa1"
  infrastructure:
    - name: "MongoDB"
      icon: "fas fa-database"
      color: "#47a248"
    - name: "FAISS Index"
      icon: "fas fa-layer-group"
      color: "#ff9800"
    - name: "File System"
      icon: "fas fa-folder"
      color: "#9c27b0"
---

## Tổng quan

Hệ thống hỏi đáp dựa trên tài liệu, sử dụng RAG (Retrieval-Augmented Generation) và AI để trả lời câu hỏi từ nội dung tài liệu.

## Kiến trúc hệ thống

- **Backend**: API REST với FastAPI, xử lý bất đồng bộ
- **Frontend**: SPA với React, giao tiếp với backend qua REST API
- **Lưu trữ**: MongoDB cho metadata, FAISS cho vector embeddings, file system cho tài liệu gốc

## Các module chính

### 1. Xác thực và phân quyền

- Đăng ký/đăng nhập với JWT
- Phân quyền admin
- Bảo vệ route và endpoint

### 2. Quản lý tài liệu

- Upload PDF, DOCX, Markdown, TXT
- Parse và tách thành chunks
- Lưu metadata trong MongoDB
- Quản lý tài liệu theo user

### 3. Embedding và Vector Search

- Tạo embeddings bằng OpenAI hoặc Sentence Transformers
- Lưu vector trong FAISS index (mỗi tài liệu một index)
- Hỗ trợ batch processing
- Lưu metadata mapping trong MongoDB

### 4. RAG (Retrieval-Augmented Generation)

- Embed câu hỏi và tìm kiếm vector similarity
- Lấy top-k chunks liên quan
- Tạo câu trả lời bằng LLM (OpenAI/Gemini)
- Trả về câu trả lời kèm references

### 5. Lịch sử hỏi đáp

- Lưu lịch sử câu hỏi/trả lời
- Lọc theo tài liệu
- Xem và quản lý lịch sử
- Hiển thị references và similarity scores

### 6. Tạo Quiz tự động

- Tạo câu hỏi từ tài liệu bằng LLM
- Hỗ trợ nhiều loại câu hỏi
- Chế độ Practice và Test
- Hiển thị kết quả và giải thích

### 7. Tích hợp Google Calendar

- Kết nối tài khoản Google Calendar
- Tạo sự kiện từ quiz/test
- Quản lý lịch học
- Mã hóa credentials

### 8. Admin Dashboard

- Quản lý người dùng
- Xem thống kê hệ thống
- Quản lý tài liệu
- Theo dõi hoạt động

## Luồng xử lý chính

### Upload và xử lý tài liệu

1. User upload → lưu file gốc
2. Parse nội dung → tách chunks
3. Tạo embeddings → lưu vào FAISS
4. Cập nhật metadata trong MongoDB

### Hỏi đáp với RAG

1. User đặt câu hỏi
2. Embed câu hỏi
3. Tìm kiếm vector similarity trong FAISS
4. Lấy top-k chunks liên quan
5. Ghép context → gọi LLM
6. Trả về câu trả lời + references
7. Lưu vào lịch sử

## Tính năng nổi bật

- Hỗ trợ nhiều định dạng tài liệu
- Embedding linh hoạt (OpenAI/local)
- LLM đa provider (OpenAI/Gemini)
- Tìm kiếm vector nhanh với FAISS
- Bảo mật JWT và phân quyền
- Giao diện responsive
- Tích hợp Google Calendar
- Tạo quiz tự động

## Bảo mật

- Xác thực JWT
- Mã hóa mật khẩu với bcrypt
- Phân quyền admin
- CORS
- Mã hóa credentials Google Calendar

## Hiệu năng

- Xử lý bất đồng bộ
- Batch processing cho embeddings
- FAISS cho tìm kiếm vector nhanh
- Tối ưu context length cho LLM

Dự án phù hợp cho ứng dụng học tập, nghiên cứu và quản lý tài liệu với AI.
