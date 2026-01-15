# Bài 2: Cải thiện lặp lại (Iterative Refinement)

## 🎯 Mục tiêu bài học

- Thành thạo cách tiếp cận theo chu kỳ với AI.
- Biết cách tinh chỉnh kết quả qua nhiều lượt hội thoại.
- Xây dựng các tính năng phức tạp một cách vững chắc.

---

## Cải thiện lặp lại là gì?

Thay vì cố gắng viết một Prompt hoàn hảo ngay từ lần đầu → Hãy chia nhỏ thành **nhiều lượt (iterations)**, mỗi lượt sẽ làm tốt hơn lượt trước hoặc thêm một tính năng mới.

```
Lượt 1: Triển khai khung cơ bản (MVP)
    ↓
Lượt 2: Thêm xử lý lỗi và validate
    ↓
Lượt 3: Tối ưu hiệu suất và Clean code
    ↓
Lượt 4: Hoàn thiện UI và các trường hợp biên (Edge cases)
```

---

## Tại sao nên làm lặp lại?

### Lợi ích:

- ✅ **Dễ kiểm soát**: Bạn có thể điều chỉnh hướng đi ngay lập tức nếu AI hiểu sai.
- ✅ **Chất lượng cao hơn**: AI không bị quá tải bởi quá nhiều yêu cầu cùng lúc.
- ✅ **Học hỏi**: Bạn thấy được cách AI xây dựng code từ thấp đến cao.
- ✅ **Phản hồi nhanh**: Bạn có mã nguồn chạy được ngay từ những lượt đầu tiên.

---

## Các chiến lược lặp lại hiệu quả

### Chiến lược 1: Bồi đắp dần (Build Up)

Bắt đầu từ cái cốt lõi, sau đó đắp thêm thịt.

- **Lượt 1:** "Tạo một form liên hệ cơ bản với ô Tên và Email."
- **Lượt 2:** "Thêm validation: Email phải đúng định dạng, Tên không được để trống."
- **Lượt 3:** "Thêm trạng thái loading và vô hiệu hóa nút gửi khi đang xử lý."
- **Lượt 4:** "Hiển thị thông báo Toast thành công hoặc thất bại sau khi gửi."

### Chiến lược 2: Vòng lặp Phản hồi (Feedback Loop)

Nhận kết quả, đưa ra nhận xét cụ thể để AI sửa.

- **Prompt của bạn:** "Tạo một component bảng dữ liệu."
- **AI trả về:** [Một cái bảng cơ bản]
- **Phản hồi của bạn:** "Tốt rồi! Bây giờ hãy:
  - Thêm tính năng sắp xếp khi click vào tiêu đề cột.
  - Phân trang 10 dòng mỗi trang."

---

## Cách đưa ra phản hồi hiệu quả

### Tránh các câu chung chung:

- ❌ "Làm cho nó tốt hơn đi."
- ❌ "Vẫn chưa đúng ý tôi."

### Hãy dùng các câu cụ thể:

- ✅ "Phần logic tính toán đúng rồi, nhưng hãy đổi cách hiển thị tiền tệ sang VNĐ."
- ✅ "Hãy dùng thư viện Zod thay vì dùng regex thủ công cho phần validate này."
- ✅ "Đoạn code này hơi rối, hãy chia nhỏ nó ra thành các component con."

---

## 📝 Bài tập thực hành

### Bài tập 1: Lập kế hoạch lặp lại

Yêu cầu: Xây dựng hệ thống bình luận (Comment system).
Hãy viết kế hoạch 4 bước lặp lại từ đơn giản đến phức tạp.

### Bài tập 2: Thực hành sửa lỗi lặp lại

Hãy đưa cho AI một đoạn code có lỗi. Khi AI đưa ra cách sửa, hãy cố tình tìm ra một điểm chưa tối ưu và yêu cầu AI sửa tiếp lượt 2. Quan sát sự thay đổi.

---

**← Bài trước:** [Chain of Thought](./lesson-01-chain-of-thought.md)
**Bài tiếp theo →** [Bài 3: Quản lý Ngữ cảnh (Context Management)](./lesson-03-context-management.md)
