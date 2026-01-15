# Dự án 2: Xây dựng REST API cùng AI

## 🎯 Mục tiêu

Xây dựng một hệ thống API Backend hoàn chỉnh cho nền tảng Blog.
Kỹ năng luyện tập: Thiết kế API, Database, Xác thực người dùng, và Kiểm thử.

---

## Chuỗi các câu lệnh mẫu (Prompts Sequence)

### 📐 Giai đoạn 1: Thiết kế

#### Prompt 1.1: Đặc tả API (OpenAPI)

```
Tôi muốn xây dựng API cho một trang Blog.
Yêu cầu:
- Resources: Users, Posts, Comments, Categories.
- Mỗi Post có tác giả, danh mục và nhiều tags.
- Người dùng có thể bình luận vào bài viết.

Hãy thiết kế danh sách các endpoints chuẩn RESTful.
```

#### Prompt 1.2: Thiết kế Database

```
Từ danh sách API trên, hãy thiết kế Schema cho PostgreSQL sử dụng Prisma ORM.
Yêu cầu định nghĩa rõ các quan hệ 1-nhiều và nhiều-nhiều.
```

---

### 🏗️ Giai đoạn 2: Triển khai

#### Prompt 2.1: Khởi tạo dự án

```
Hãy giúp tôi setup một dự án Express.js với TypeScript và Prisma.
Cung cấp cấu trúc thư mục phân lớp (Controller, Service, Repository).
```

#### Prompt 2.2: Triển khai xác thực (Authentication)

```
Viết logic đăng ký và đăng nhập sử dụng thư viện `bcrypt` và `jsonwebtoken`.
Triển khai một middleware tên là `authGuard` để bảo vệ các API yêu cầu đăng nhập.
```

---

### 🧪 Giai đoạn 3: Kiểm thử và Bảo mật

#### Prompt 3.1: Viết Unit Test cho Service

```
Hãy viết unit test cho `PostService`, giả lập (mock) Prisma client để kiểm tra logic tạo bài viết và kiểm tra quyền sở hữu.
```

---

## Tiêu chí thành công

- [ ] API hoạt động đúng chuẩn REST (dùng đúng mã HTTP: 200, 201, 400, 401...).
- [ ] Mật khẩu được bảo mã hóa an toàn.
- [ ] Dữ liệu đầu vào được validate chặt chẽ (dùng Zod hoặc Joi).
- [ ] Có tài liệu API đầy đủ.
