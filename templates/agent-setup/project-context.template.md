# [Tên Dự Án]

## Mô tả ngắn gọn

[1-2 câu mô tả dự án làm gì, phục vụ đối tượng nào]

---

## Tech Stack

| Layer    | Công nghệ                           |
| -------- | ----------------------------------- |
| Frontend | [React 18, Next.js 14, TailwindCSS] |
| Backend  | [Node.js 20, Express 4, TypeScript] |
| Database | [PostgreSQL 15, Prisma ORM]         |
| Cache    | [Redis]                             |
| Auth     | [JWT, NextAuth.js]                  |
| Testing  | [Jest, React Testing Library]       |
| Deploy   | [Docker, AWS ECS, Vercel]           |

---

## Cấu trúc thư mục chính

```
src/
├── app/              # Next.js App Router (pages, layouts)
├── components/       # UI Components tái sử dụng
│   ├── ui/           # Primitive components (Button, Input, Card)
│   └── features/     # Feature-specific components
├── features/         # Business logic theo từng tính năng
├── hooks/            # Custom React hooks
├── services/         # API client và external services
├── lib/              # Utilities và helpers
├── types/            # TypeScript global types
└── styles/           # Global styles
```

---

## Trạng thái hiện tại (Cập nhật: [NGÀY])

### ✅ Đã hoàn thành

- [x] Authentication (Đăng nhập, Đăng ký, Quên mật khẩu)
- [x] User Profile Management
- [x] Base UI Component Library

### 🔄 Đang thực hiện

- [ ] Product Catalog
  - [x] Listing page
  - [x] Detail page
  - [ ] Search & Filter (đang làm)
  - [ ] Pagination

### 📋 Chưa bắt đầu

- [ ] Shopping Cart
- [ ] Checkout & Payment
- [ ] Order Management
- [ ] Admin Dashboard

---

## Lưu ý quan trọng khi làm việc

1. **TypeScript Strict Mode:** Mọi file đều phải có types rõ ràng, không dùng `any`.
2. **API Calls:** Mọi request đều phải đi qua `src/services/`, không gọi `fetch` trực tiếp trong components.
3. **Error Handling:** Sử dụng `try-catch` và custom `AppError` class.
4. **Git Workflow:** Không commit thẳng vào `main`. Tạo branch `feature/*` hoặc `fix/*`.
5. **Testing:** Mỗi feature mới cần có unit test với coverage tối thiểu 70%.

---

## Các file/folder quan trọng cần biết

| File/Folder              | Mục đích                        |
| ------------------------ | ------------------------------- |
| `prisma/schema.prisma`   | Database schema                 |
| `src/lib/api-client.ts`  | Axios instance với interceptors |
| `src/hooks/useAuth.ts`   | Hook quản lý authentication     |
| `src/types/api.types.ts` | Types cho API request/response  |
| `.env.example`           | Mẫu biến môi trường             |
