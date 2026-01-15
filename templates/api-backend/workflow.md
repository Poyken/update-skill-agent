# Quy trình phát triển API Backend cùng AI

## Giai đoạn 1: Thiết kế API

### Bước 1.1: Đặc tả Endpoint

- **Prompt mẫu:** "Thiết kế các API endpoints cho hệ thống [tên hệ thống]. Tài nguyên gồm: [User, Post...]. Với mỗi endpoint, hãy nêu rõ Path, Method, dữ liệu gửi lên (Request Body) và cấu trúc phản hồi mẫu (Response)."

### Bước 1.2: Thiết kế Cơ sở dữ liệu

- **Prompt mẫu:** "Dựa trên các API đã thiết kế, hãy tạo sơ đồ quan hệ database (ERD) và viết script SQL để khởi tạo các bảng, đảm bảo các ràng buộc về khóa ngoại (Foreign Keys) và đánh index cho các trường tìm kiếm thường xuyên."

---

## Giai đoạn 2: Triển khai

### Bước 2.1: Xác thực & Phân quyền (Auth)

- **Prompt mẫu:** "Triển khai hệ thống đăng nhập sử dụng JWT (JSON Web Token) cho [Express/NestJS]. Yêu cầu: Password phải được băm (hash), có hỗ trợ Refresh Token và middleware để bảo vệ các route riêng tư."

### Bước 2.2: Xử lý nghiệp vụ (Business Logic)

- **Prompt mẫu:** "Hãy viết service xử lý việc [tên nghiệp vụ, ví dụ: thanh toán đơn hàng]. Yêu cầu phải sử dụng Database Transaction để đảm bảo tính toàn vẹn dữ liệu khi có lỗi xảy ra."

---

## Giai đoạn 3: Bảo mật & Kiểm thử

### Bước 3.1: Bảo mật và Tối ưu

- **Prompt mẫu:** "Hãy review code này và đề xuất các biện pháp bảo mật: Chống SQL Injection, Rate Limiting, và cấu hình các Security Headers cần thiết."

### Bước 3.2: Viết Integration Test

- **Prompt mẫu:** "Hãy viết test case sử dụng Supertest để kiểm tra luồng tạo đơn hàng, bao gồm cả các trường hợp thanh toán thất bại."
