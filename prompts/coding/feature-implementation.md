# Prompt mẫu để triển khai Tính năng (Feature Implementation)

## 1. Yêu cầu tính năng cơ bản

```
Triển khai tính năng [tên tính năng] có chức năng [mô tả chức năng].

Yêu cầu cụ thể:
- [Yêu cầu 1]
- [Yêu cầu 2]
- [Yêu cầu 3]

Công nghệ sử dụng: [framework/thư viện]
Tiêu chuẩn code: [convention hoặc phong cách viết code]
```

### Ví dụ:

```
Triển khai tính năng xác thực người dùng cho phép đăng nhập bằng email/mật khẩu.

Yêu cầu cụ thể:
- Kiểm tra định dạng email hợp lệ
- Mật khẩu tối thiểu 8 ký tự
- Hiển thị thông báo lỗi khi thông tin không chính xác
- Chuyển hướng về trang Dashboard sau khi đăng nhập thành công

Công nghệ sử dụng: React + React Hook Form
Tiêu chuẩn code: Sử dụng TypeScript, tuân theo Airbnb style guide
```

---

## 2. Tạo Component (Giao diện)

```
Tạo một component [loại component] tên là [TênComponent] với các yêu cầu:

Props:
- [prop1]: [kiểu dữ liệu] - [mô tả]
- [prop2]: [kiểu dữ liệu] - [mô tả]

State (Trạng thái):
- [state1]: [mô tả]

Sự kiện (Events):
- [event1]: [khi nào kích hoạt]

Giao diện (UI):
- [Mô tả ngoại hình, màu sắc, bố cục]

Yêu cầu đi kèm: Bao gồm TypeScript types và unit tests.
```

### Ví dụ:

```
Tạo một ActionButton component với các yêu cầu:

Props:
- label: string - Nội dung hiển thị trên nút
- variant: 'primary' | 'secondary' | 'danger' - Kiểu dáng nút
- isLoading: boolean - Hiển thị spinner khi đang tải
- onClick: () => void - Hàm xử lý khi click

UI:
- Bo góc, kích thước trung bình
- Màu sắc thay đổi theo từng variant
- Làm mờ (disabled) khi đang ở trạng thái loading

Yêu cầu đi kèm: Viết unit tests bằng React Testing Library.
```

---

## 3. Tạo API Endpoint

```
Tạo một REST API endpoint:

Endpoint: [METHOD] /api/[đường dẫn]

Yêu cầu Request:
- Headers: [các header bắt buộc]
- Body: [schema dữ liệu gửi lên]

Yêu cầu Response (Phản hồi):
- Thành công (200/201): [dữ liệu phản hồi]
- Các trường hợp lỗi:
  - 400: [khi nào]
  - 401: [khi nào]
  - 404: [khi nào]

Logic nghiệp vụ (Business Logic):
1. [bước 1]
2. [bước 2]

Yêu cầu: Bao gồm validation dữ liệu và xử lý lỗi chặt chẽ.
```

---

## 4. Thiết kế Database Model

```
Tạo database model cho thực thể [tên thực thể]:

Các trường (Fields):
- [field1]: [kiểu dữ liệu] - [ràng buộc/constraints]
- [field2]: [kiểu dữ liệu] - [ràng buộc/constraints]

Quan hệ (Relationships):
- [Mô tả quan hệ với các bảng khác]

Indexes:
- [Các trường cần đánh index]

Yêu cầu: Cung cấp script migration cho [tên database, ví dụ: PostgreSQL].
```
