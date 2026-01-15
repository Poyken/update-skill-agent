# Bài 3: Quản lý Ngữ cảnh (Context Management)

## 🎯 Mục tiêu bài học

- Học cách cung cấp thông tin "đủ và đúng" cho AI.
- Tránh việc AI bị quá tải thông tin (Context window limit).
- Tối đa hóa khả năng hiểu của AI về dự án của bạn.

---

## Ngữ cảnh (Context) là gì?

### Context = Bộ nhớ của AI

- AI chỉ biết những gì bạn đã nói trong cuộc hội thoại hiện tại.
- AI không thể "nhìn thấy" toàn bộ code trong máy tính của bạn trừ khi bạn đính kèm hoặc dán nó vào.
- **Context càng sạch và liên quan = Kết quả càng chính xác.**

---

## Chiến lược quản lý Ngữ cảnh

### Chiến lược 1: Chỉ cung cấp những gì liên quan

Đừng dán cả file 2000 dòng nếu bạn chỉ định sửa một hàm 10 dòng.

- ❌ Dán toàn bộ file.
- ✅ Dán hàm cần sửa + Các hàm liên quan trực tiếp + Types liên quan.

### Chiến lược 2: Tóm tắt những phần không quan trọng

Thay vì dán full code của hệ thống Auth (đã chạy tốt), hãy nói bằng lời:

> "Dự án của tôi đang dùng JWT để xác thực (đã chạy ổn định). Bây giờ hãy tập trung vào tính năng mới này: [dán code tính năng mới]."

### Chiến lược 3: Quản lý cuộc hội thoại dài

Khi chat quá dài, AI bắt đầu "quên" các thông tin ở đầu hoặc bắt đầu nhầm lẫn.

- **Giải pháp:** Sau khoảng 10-15 câu lệnh, hãy tóm tắt lại những gì đã làm được và bắt đầu một phiên chat mới nếu cần.
  > "Tóm tắt: Chúng ta đã tạo xong bảng User và API đăng ký. Bây giờ hãy bắt đầu làm API đăng nhập."

---

## Những thông tin NÊN đính kèm:

### Luôn luôn có ✅

- Công nghệ & Phiên bản (ví dụ: Next.js 14, Tailwind v3).
- Ngôn ngữ (TypeScript, Go, Python...).
- Đoạn code cụ thể đang làm việc.
- Thông báo lỗi đầy đủ.
- Mục tiêu bạn muốn đạt được.

### Đính kèm khi cần thiết

- Schema của Database (khi làm việc với dữ liệu).
- File `package.json` (khi gặp lỗi về phiên bản thư viện).
- File cấu hình (khi gặp lỗi về build/environment).

---

## 📝 Bài tập thực hành

### Bài tập 1: Thu gọn ngữ cảnh

Bạn có một file code lớn. Hãy thử trích xuất ra những phần **tối thiểu nhất** cần thiết để AI có thể:

1. Viết Unit Test cho một hàm trong file đó.
2. Thêm một logic mới vào giữa file.

### Bài tập 2: Tóm tắt tiến độ

Sau khi đã làm việc với AI một lúc, hãy thử yêu cầu: _"Hãy tóm tắt lại các yêu cầu và tiến độ dự án mà chúng ta đã thống nhất từ đầu đến giờ"_. Kiểm tra xem AI có hiểu đúng ý bạn không.

---

**← Bài trước:** [Cải thiện lặp lại](./lesson-02-iterative-refinement.md)
**Bài tiếp theo →** [Module 4: Dự án thực tế](../04-real-projects/)
