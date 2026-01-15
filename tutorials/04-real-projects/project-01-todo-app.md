# Dự án 1: Xây dựng Todo App cùng AI

## 🎯 Mục tiêu

Xây dựng một ứng dụng Todo hoàn chỉnh **chỉ bằng cách sử dụng các câu lệnh (prompts)**.
Mục tiêu là luyện tập quy trình: Từ ý tưởng → Thiết kế → Triển khai → Hoàn thiện.

---

## Chuỗi các câu lệnh mẫu (Prompts Sequence)

### 🔧 Giai đoạn 1: Thiết lập (Setup)

#### Prompt 1.1: Khởi tạo dự án

```
Hãy giúp tôi khởi tạo một dự án React mới sử dụng Vite và TypeScript.

Yêu cầu:
- React 18 + TypeScript.
- TailwindCSS để định dạng giao diện.
- Sử dụng npm.

Hãy cung cấp các lệnh terminal cần chạy và các file cấu hình cơ bản.
```

---

### 🏗️ Giai đoạn 2: Triển khai (Implementation)

#### Prompt 2.1: Thiết kế dữ liệu và State

```
Tôi muốn xây dựng ứng dụng Todo với các tính năng: Thêm, sửa, xóa, đánh dấu hoàn thành, lọc theo trạng thái.

Hãy thiết kế:
1. TypeScript interfaces cho Todo item.
2. Một custom hook tên là `useTodos` để quản lý logic (CRUD) và lưu dữ liệu vào localStorage.
```

#### Prompt 2.2: Xây dựng giao diện (UI)

```
Hãy tạo các React components sau bằng TailwindCSS:
1. `TodoInput`: Ô nhập task mới, có nút Add và hỗ trợ phím Enter.
2. `TodoItem`: Hiển thị một task, có nút Delete và checkbox để hoàn thành.
3. `TodoList`: Danh sách bao bọc các item, hiển thị thông báo khi danh sách trống.

Yêu cầu giao diện hiện đại, sạch sẽ và có hiệu ứng hover.
```

---

### ✨ Giai đoạn 3: Hoàn thiện (Polish)

#### Prompt 3.1: Thêm tính năng nâng cao

```
Bây giờ hãy thêm các tính năng sau vào app:
1. Chế độ tối (Dark mode) dựa trên hệ điều hành.
2. Phân loại task theo mức độ ưu tiên (Gấp, Bình thường, Tháp).
3. Hiệu ứng chuyển cảnh mượt mà khi thêm/xóa task.
```

---

## Checklist hoàn thành dự án

- [ ] Ứng dụng chạy không có lỗi console.
- [ ] Dữ liệu vẫn còn khi tải lại trang (persistence).
- [ ] Giao diện hiển thị tốt trên cả mobile và desktop.
- [ ] Code sạch, được chia thành các component nhỏ.

---

**Bài tiếp theo →** [Dự án 2: Xây dựng REST API](./project-02-rest-api.md)
