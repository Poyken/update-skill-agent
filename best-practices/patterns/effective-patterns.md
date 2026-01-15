# Các mô hình hiệu quả khi dùng AI (Effective Patterns)

## 🎯 Mục đích

Tổng hợp các cách tiếp cận giúp bạn nhận được câu trả lời chất lượng cao nhất từ AI Agent một cách nhất quán.

---

## Mô hình 1: Ngữ cảnh là Ưu tiên số 1 (Context First) 📋

**Luôn cung cấp bối cảnh trước khi đưa ra câu hỏi.**

- **Tại sao?**: AI cần hiểu bạn đang ở đâu để đưa ra giải pháp phù hợp nhất.
- **Ví dụ**:
  - ✅ _Tốt:_ "Trong API Express.js sử dụng PostgreSQL và Prisma, tôi muốn triển khai tính năng xóa mềm (soft delete)..."
  - ❌ _Tệ:_ "Làm sao để xóa user trong database?"

---

## Mô hình 2: Show, Don't Just Tell (Cung cấp bằng chứng) 📸

**Luôn đính kèm các đoạn code hoặc log lỗi liên quan.**

- **Tại sao?**: Thay vì để AI đoán, hãy cho nó thấy thực tế. Nó sẽ đưa ra cách sửa lỗi chính xác đến từng dòng code.
- **Cách làm**: Dán đoạn code nghi ngờ lỗi + Thông báo lỗi đầy đủ (full stack trace).

---

## Mô hình 3: Xây dựng từng bước (Iterative Building) 🏗️

**Tính năng phức tạp = Nhiều prompt nhỏ liên tiếp.**

- **Tại sao?**: AI làm việc tốt nhất khi tập trung vào một vấn đề nhỏ. Việc yêu cầu quá nhiều thứ một lúc dễ khiến AI bị "loạn" hoặc bỏ sót yêu cầu.
- **Quy trình mẫu**:
  1. Tạo form cơ bản.
  2. Thêm validation.
  3. Thêm xử lý lỗi và loading state.
  4. Thêm hiệu ứng và hoàn thiện UI.

---

## Mô hình 4: Yêu cầu giải thích logic (Request Explanations) 💡

**Hãy hỏi AI "tại sao bạn làm như vậy?".**

- **Tại sao?**: Giúp bạn học hỏi được tư duy của AI, phát hiện ra các sai sót logic tiềm ẩn và hiểu rõ các đánh đổi (trade-offs).
- **Cách làm**: "Hãy triển khai giải pháp X và giải thích tại sao bạn chọn cách này thay vì cách Y."

---

## Mô hình 5: Chỉ định rõ các Ràng buộc (Specify Constraints) 🎯

**Nói rõ những gì AI "không được làm".**

- **Tại sao?**: AI thường chọn cách dễ nhất hoặc phổ biến nhất, đôi khi không phù hợp với dự án của bạn (ví dụ: dùng thư viện mà bạn không được phép cài thêm).
- **Ví dụ**: "Viết hàm xử lý ảnh nhưng **không được dùng thư viện bên ngoài**, chỉ dùng các API có sẵn của Browser."

---

## Mô hình 6: Review trước khi áp dụng (Review Before Apply) 👀

**Luôn coi code của AI là bản thảo.**

- **Checklist nhanh**:
  - [ ] Code có đúng logic không?
  - [ ] Có tuân thủ tiêu chuẩn của dự án không?
  - [ ] Có hardcode (viết cứng) các giá trị nhạy cảm không?
  - [ ] Đã có xử lý lỗi chưa?

---

## Mô hình 7: Prompt định hướng Test (Test-Driven Prompts) ✅

**Yêu cầu AI viết Unit Test kèm theo code.**

- **Tại sao?**: Code có test đi kèm thường sẽ có kiến trúc tốt hơn, dễ module hóa và ít bug hơn.

---

## Thẻ tra cứu nhanh (Quick Reference)

| Mô hình        | Câu lệnh mẫu                        | Khi nào dùng?                 |
| -------------- | ----------------------------------- | ----------------------------- |
| **Ngữ cảnh**   | "Trong dự án [Stack] của tôi..."    | Luôn luôn                     |
| **Bằng chứng** | "Đây là code và lỗi của tôi..."     | Khi debug                     |
| **Chia nhỏ**   | "Đầu tiên, hãy làm bản đơn giản..." | Khi tính năng phức tạp        |
| **Giải thích** | "Giải thích tại sao chọn cách này?" | Khi muốn học/hiểu             |
| **Ràng buộc**  | "Đừng dùng thư viện X..."           | Khi dự án có tiêu chuẩn riêng |

---

**Xem thêm:** [Các sai lầm cần tránh (Anti-Patterns)](./anti-patterns.md)
