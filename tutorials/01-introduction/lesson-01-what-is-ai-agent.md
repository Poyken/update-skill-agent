# Bài 1: AI Agent là gì?

## 🎯 Mục tiêu học tập

Sau bài học này, bạn sẽ:

- Hiểu AI Agent trong bối cảnh lập trình là gì.
- Phân biệt được AI Agent với các công cụ lập trình truyền thống.
- Biết các khả năng chính (capabilities) của một AI coding agent.

---

## AI Agent so với Công cụ Truyền thống

| Khía cạnh               | IDE truyền thống                  | AI Agent                                   |
| ----------------------- | --------------------------------- | ------------------------------------------ |
| **Gợi ý code**          | Dựa trên mẫu có sẵn, khớp từ khóa | Hiểu ngữ cảnh, hiểu ý nghĩa (semantic)     |
| **Sửa lỗi (Debugging)** | Thủ công, từng bước một           | Phân tích hỗ trợ, gợi ý nguyên nhân gốc rễ |
| **Cải thiện code**      | Dựa trên các quy tắc cứng         | Hiểu ý định của lập trình viên             |
| **Viết tài liệu**       | Dùng template có sẵn              | Tự tạo dựa trên code hiện có               |
| **Độ khó khi học**      | Cao cho từng công cụ riêng lẻ     | Giao tiếp bằng ngôn ngữ tự nhiên           |

---

## Các AI Agent phổ biến hiện nay

### 1. GitHub Copilot

- **Loại**: Extension cho IDE.
- **Thế mạnh**: Gợi ý code trực tiếp khi đang gõ, hiểu ngữ cảnh từ codebase.
- **Dùng tốt nhất cho**: Viết code hàng ngày, tự động hoàn thành các đoạn code lặp lại.

### 2. Cursor

- **Loại**: Một trình soạn thảo code (IDE) hoàn chỉnh dựa trên VS Code.
- **Thế mạnh**: Hiểu sâu toàn bộ dự án, có khả năng chat và sửa code trực tiếp trên nhiều file.
- **Dùng tốt nhất cho**: Refactor lớn, xây dựng tính năng phức tạp từ đầu.

### 3. Claude / ChatGPT

- **Loại**: AI hội thoại (Chatbot).
- **Thế mạnh**: Giải thích chi tiết, hỗ trợ tư duy kiến trúc, học kiến thức mới.
- **Dùng tốt nhất cho**: Thiết kế hệ thống, giải quyết các lỗi khó, học ngôn ngữ mới.

---

## AI Agent có thể làm được gì?

### ✅ Những việc AI làm rất tốt

- Tự tạo các đoạn code mẫu (boilerplate code).
- Giải thích các đoạn code cũ hoặc khó hiểu.
- Gợi ý cách sửa các lỗi phổ biến.
- Viết unit tests tự động.
- Cải thiện cấu trúc code (refactor).
- Trả lời nhanh các câu hỏi về cú pháp hoặc thư viện.

### ⚠️ Những việc cần bạn kiểm tra kỹ

- Logic nghiệp vụ (business logic) phức tạp hoặc đặc thù của công ty.
- Các đoạn code yêu cầu bảo mật cao.
- Tối ưu hóa hiệu suất ở mức cực hạn.
- Cấu hình cho môi trường Production.

### ❌ Những việc không nên giao hoàn toàn cho AI

- Ra các quyết định quan trọng về mô hình kinh doanh.
- Thiết kế kiến trúc tổng thể cho các hệ thống khổng lồ mà không có sự giám sát.
- Các vấn đề về pháp lý hoặc tuân thủ (compliance).

---

## 📝 Bài tập thực hành

### Bài tập 1: Khám phá khả năng

1. Mở một AI agent bạn đang có (Claude, ChatGPT, hoặc Copilot Chat).
2. Hỏi: _"Hãy liệt kê 10 việc bạn có thể giúp tôi với tư cách là một lập trình viên"_.
3. So sánh câu trả lời của AI với những gì bạn mong đợi.

### Bài tập 2: Tương tác đầu tiên

1. Chọn một phần việc đơn giản bạn đang định làm (ví dụ: viết hàm validate dữ liệu).
2. Mô tả yêu cầu cho AI.
3. Đánh giá: Kết quả có chạy được không? Có cần bạn sửa chỗ nào không?

---

## 🔑 Những điều cần nhớ

1. AI Agent là **công cụ hỗ trợ**, không phải là người thay thế bạn.
2. **Ngữ cảnh (Context) là quan trọng nhất** - bạn cung cấp càng nhiều thông tin, kết quả càng tốt.
3. **Luôn kiểm tra lại code** - đừng bao giờ copy và chạy mà không đọc hiểu.
4. **Cải thiện dần dần** - một câu lệnh đầu tiên có thể chưa hoàn hảo, hãy học cách điều chỉnh nó.

---

**Bài tiếp theo →** [Bài 2: Khi nào nên dùng AI Agent](./lesson-02-when-to-use.md)
