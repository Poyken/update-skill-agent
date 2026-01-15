# Bài 1: Khung CLEAR - Bí quyết viết Prompt chuẩn cho Dev

## 🎯 Mục tiêu bài học

- Nắm vững khung CLEAR để xây dựng prompt.
- Biết cách cấu trúc một câu lệnh chuyên nghiệp.
- Tránh các lỗi mơ hồ khiến AI đưa ra kết quả kém.

---

## Khung CLEAR (CLEAR Framework)

Để AI làm việc hiệu quả nhất, một prompt nên bao gồm 5 yếu tố sau:

### C - Context (Ngữ cảnh / Bối cảnh)

Cho AI biết bạn đang làm việc trong môi trường nào, dự án gì.

- Dự án là gì?
- Bạn đang gặp khó khăn gì?
- Đối tượng sử dụng code này là ai?

### L - Language / Stack (Ngôn ngữ / Công nghệ)

Chỉ định rõ ngôn ngữ lập trình và các thư viện liên quan.

- Phiên bản ngôn ngữ/framework?
- Bạn có muốn dùng thư viện cụ thể nào không?

### E - Expectation (Kỳ vọng / Kết quả mong muốn)

Mô tả rõ bạn muốn nhận lại cái gì từ AI.

- Bạn muốn code hoàn chỉnh hay chỉ giải thích?
- Bạn có cần viết kèm unit test không?
- Định dạng output (Markdown, JSON, Code...)

### A - Action (Hành động cụ thể)

Lệnh yêu cầu AI phải thực hiện.

- Hãy dùng các động từ mạnh: "Viết hàm...", "Sửa lỗi...", "Tối ưu hóa...", "Giải thích...".
- Chia nhỏ các bước nếu hành động quá phức tạp.

### R - Restrictions (Ràng buộc / Giới hạn)

Các điều kiện mà AI không được vi phạm.

- Không dùng thư viện X.
- Code phải tương thích với trình duyệt Y.
- Giới hạn số dòng hoặc phong cách viết code (ví dụ: Functional Programming).

---

## Ví dụ thực tế

### ❌ Prompt Tồi (Mơ hồ)

> "Viết cho tôi hàm đăng nhập"

**Vấn đề:**

- Thiếu ngữ cảnh (Frontend hay Backend?)
- Không biết dùng công nghệ gì.
- Không biết cần hỗ trợ những gì (validate, token?).

---

### ✅ Prompt Tốt (Áp dụng CLEAR)

```
**Context (C):**
Tôi đang xây dựng một ứng dụng Next.js 14 và cần tích hợp tính năng đăng nhập.

**Language/Stack (L):**
TypeScript, thư viện NextAuth.js v5, sử dụng Prisma ORM kết nối PostgreSQL.

**Expectation (E):**
Hãy viết code cho API route xử lý đăng nhập và cung cấp tài liệu ngắn gọn về cách cấu hình.

**Action (A):**
Triển khai endpoint POST /api/auth/login thực hiện:
1. Validate email và mật khẩu (dùng Zod).
2. Kiểm tra tài khoản trong database.
3. Trả về JWT token nếu thành công.

**Restrictions (R):**
- Sử dụng bcrypt để mã hóa và so sánh mật khẩu.
- Không được trả về thông tin mật khẩu của người dùng trong response.
- Giới hạn tối đa 5 lần thử đăng nhập/phút để tránh Brute Force.
```

---

## 📝 Bài tập thực hành

### Bài tập 1: Viết lại Prompt

Hãy áp dụng khung CLEAR để viết lại các prompt sau:

1. "Hãy giúp tôi viết thuật toán sắp xếp mảng."
2. "Làm thế nào để code nhanh hơn?"
3. "Sửa lỗi crash này cho tôi."

### Bài tập 2: Tự áp dụng

Chọn một task bạn đang thực sự phải làm trong dự án hiện tại. Hãy viết prompt theo đúng 5 bước CLEAR và quan sát sự khác biệt của câu trả lời từ AI.

---

## 🔑 Những điều cần nhớ

1. **Cấu trúc tốt = Kết quả tốt** - Đầu tư 1 phút viết prompt giúp tiết kiệm 10 phút sửa code.
2. **Cụ thể là sức mạnh** - AI không biết "đọc tâm trí" của bạn, hãy nói rõ bạn muốn gì.
3. **Luôn đặt ngữ cảnh lên đầu** - AI cần biết nó đang đóng vai trò gì trong dự án của bạn.

---

**Bài tiếp theo →** [Bài 2: Các mẫu Prompt phổ biến](./lesson-02-common-patterns.md)
