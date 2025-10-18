# AI4ALL - Artificial Intelligent For All-of-us

Trang blog chia sẻ kiến thức về AI, Machine Learning, Deep Learning, Backend Development và các dự án cá nhân.

## 👥 Tác giả

- **Baro**  - Author
- **Hieu** - Author

## 🚀 Giới thiệu

AI4ALL là nơi chúng tôi chia sẻ:
- Kiến thức về Deep Learning, Neural Networks, Computer Vision
- Hướng dẫn Backend Development với Python, FastAPI, Node.js
- Các dự án AI thực tế và case studies
- Kinh nghiệm học tập và nghiên cứu

## 📝 Hướng dẫn viết bài

### Cấu trúc file bài viết

Tất cả bài viết được lưu trong thư mục `_posts/` với tên file theo format:
```
YYYY-MM-DD-ten-bai-viet.md
```

Ví dụ: `2025-10-14-neural-networks-explained.md`

### Template bài viết cơ bản

```markdown
---
layout: post
title: "Tiêu đề bài viết của bạn"
date: 2025-10-14 14:30:00 +0700
author: baro
categories: [deep-learning, neural-networks]
tags: [AI, machine-learning, tutorial]
image: https://link-to-your-cover-image.jpg
excerpt: "Mô tả ngắn gọn về bài viết (hiển thị trong preview)"
---

## Giới thiệu

Nội dung giới thiệu về chủ đề...

## Phần 1: Tiêu đề phần

Nội dung chi tiết...

### Tiểu mục

Giải thích chi tiết hơn...

```python
# Code example
def hello_world():
    print("Hello AI4ALL!")
```

## Kết luận

Tóm tắt và kết luận...

---
```

### Các trường quan trọng trong Front Matter

- **layout**: Luôn dùng `post`
- **title**: Tiêu đề bài viết (bắt buộc)
- **date**: Ngày giờ đăng bài theo format `YYYY-MM-DD HH:MM:SS +0700`
- **author**: `baro` hoặc `hieu` (phải khớp với tên trong `_config.yml`)
- **categories**: Danh mục chính (ví dụ: `deep-learning`, `backend`, `projects`)
- **tags**: Từ khóa liên quan
- **image**: URL ảnh đại diện (hiển thị ở trang chủ và đầu bài)
- **excerpt**: Mô tả ngắn (tối đa 2-3 câu)

### Categories thường dùng

- `deep-learning` - Các bài về Deep Learning
- `machine-learning` - Machine Learning cơ bản
- `computer-vision` - Thị giác máy tính
- `nlp` - Xử lý ngôn ngữ tự nhiên
- `backend` - Backend Development
- `projects` - Các dự án thực tế
- `tutorial` - Hướng dẫn chi tiết

### Quy tắc viết bài

1. **Cấu trúc rõ ràng**: Dùng heading `##`, `###` để phân chia nội dung

2. **Code blocks**: 
   - **Quan trọng**: Code phải nằm giữa 3 dấu backtick (```)
   - Luôn ghi rõ ngôn ngữ sau backtick đầu để có syntax highlighting
   - Giữ nguyên thụt lề của code (đặc biệt với Python)
   
   Ví dụ:
   ````markdown
   ```python
   def hello_world():
       print("Hello AI4ALL!")
   ```
   ````
   
   Các ngôn ngữ được hỗ trợ:
   - `python` - Python code
   - `javascript` hoặc `js` - JavaScript
   - `java` - Java
   - `bash` hoặc `shell` - Shell commands
   - `sql` - SQL queries
   - `json` - JSON data
   - `html` - HTML markup
   - `css` - CSS styles
   
3. **Ảnh minh họa**: Dùng markdown syntax
   ```markdown
   ![Mô tả ảnh](URL-hoặc-đường-dẫn-ảnh)
   ```

4. **Định dạng văn bản**:
   - **In đậm**: `**text**`
   - *In nghiêng*: `*text*`
   - `Code inline`: `` `code` ``
   - > Trích dẫn: `> text`

5. **Công thức toán học** (dùng KaTeX):
   - Inline: `$E = mc^2$`
   - Block:
   ```markdown
   $$
   f(x) = \sum_{i=1}^{n} w_i x_i + b
   $$
   ```

### 🎨 Styling Features

Website có các tính năng giao diện đẹp:

- **VS Code-like Syntax Highlighting**: Code blocks có màu sắc giống VS Code Dark theme
- **Language Badge**: Tự động hiển thị nhãn ngôn ngữ ở góc code block
- **Responsive Design**: Tối ưu cho cả desktop và mobile
- **Dark/Light Mode**: Tự động chuyển đổi theo theme hệ thống

### Ví dụ bài viết hoàn chỉnh

Xem file: `_posts/2025-10-14-neural-networks-explained.markdown`

## 🛠️ Chạy local

```bash
# Cài đặt dependencies
bundle install

# Chạy server local
bundle exec jekyll serve

# Truy cập: http://localhost:4000
```

## 📦 Deploy

Website tự động deploy lên GitHub Pages khi push code lên nhánh `main`.

### Cấu hình cho custom domain

1. Trong `_config.yml`, đặt `baseurl: ''` (để rỗng cho custom domain)
2. Nếu deploy với repo URL, dùng `baseurl: '/ai4all'`
3. Tạo file `CNAME` với nội dung là domain của bạn (nếu dùng custom domain)
4. Cấu hình DNS:
   - A record trỏ về IP GitHub Pages: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - Hoặc CNAME record trỏ về `username.github.io`

### Xử lý conflict khi push

Nếu gặp lỗi "non-fast-forward", chạy:
```bash
git pull origin main --rebase
git push origin main
```



## 📧 Liên hệ

- Email: ai4all@gmail.com

---

**Mục đích**: Trang web này được tạo ra để ôn tập, lưu trữ và chia sẻ kiến thức về AI, backend, và các dự án cá nhân.
