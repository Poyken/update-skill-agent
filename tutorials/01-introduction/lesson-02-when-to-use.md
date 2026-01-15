# Bài 2: Khi nào nên dùng AI Agent?

## 🎯 Mục tiêu bài học

- Biết xác định thời điểm AI có thể giúp bạn hiệu quả nhất.
- Hiểu các giới hạn và những lúc không nên dùng AI.
- Xây dựng quy trình làm việc (workflow) kết hợp AI thông minh.

---

## Khi nào AI Agent hữu ích nhất?

### 🟢 Các công việc có giá trị cao (Nên dùng AI)

| Công việc                      | Tại sao AI lại tốt?                  | Ví dụ thực tế                                             |
| ------------------------------ | ------------------------------------ | --------------------------------------------------------- |
| **Code lặp lại (Boilerplate)** | Có tính quy luật, định nghĩa rõ ràng | Tạo CRUD, validate form, tạo schema                       |
| **Chuyển đổi ngôn ngữ**        | Giỏi về cấu trúc ngôn ngữ            | Chuyển JS → TS, chuyển từ thư viện này sang thư viện khác |
| **Viết tài liệu (Docs)**       | Có cấu trúc, dựa trên template       | JSDoc, README, tài liệu API                               |
| **Tạo Unit Test**              | Dựa trên mẫu thử                     | Viết test cho các hàm xử lý logic thuần túy               |
| **Giải thích/Học tập**         | Kho kiến thức khổng lồ               | "Giải thích cách hoạt động của async/await"               |
| **Sửa lỗi nhanh**              | Nhận diện mẫu lỗi tốt                | Phân tích lỗi từ log console hoặc stack trace             |

### 🟡 Các công việc ở mức trung bình (Dùng kèm sự giám sát)

| Công việc                  | Lưu ý khi dùng AI                                                             |
| -------------------------- | ----------------------------------------------------------------------------- |
| **Xây dựng tính năng mới** | AI giúp dựng khung nhanh, nhưng bạn cần kiểm soát logic nghiệp vụ.            |
| **Refactor (Tối ưu code)** | AI làm rất tốt, nhưng đôi khi quên mất các quy chuẩn riêng của dự án bạn.     |
| **Tích hợp API**           | AI hiểu các API phổ biến, nhưng cần kiểm tra lại phiên bản thư viện hiện tại. |

### 🔴 Những việc cần cực kỳ cẩn thận

| Công việc                  | Tại sao cần cẩn thận?                                                      |
| -------------------------- | -------------------------------------------------------------------------- |
| **Code liên quan bảo mật** | AI có thể vô tình tạo ra các lỗ hổng (vulnerability).                      |
| **Thuật toán cực khó**     | Kết quả AI đưa ra có thể không phải là tối ưu nhất.                        |
| **Config cho Production**  | Dễ rò rỉ thông tin bí mật (secret keys) hoặc nhầm lẫn giữa các môi trường. |

---

## Sai lầm thường gặp: Khi KHÔNG nên dùng AI

### ❌ Thiếu ngữ cảnh

- _Sai:_ "Sửa lỗi này cho tôi" (mà không đưa code hay log lỗi).
- _Đúng:_ Cung cấp đoạn code và thông báo lỗi cụ thể.

### ❌ Yêu cầu quá tham lam

- _Sai:_ "Hãy xây dựng cho tôi một sàn thương mại điện tử hoàn chỉnh".
- _Đúng:_ Chia nhỏ thành: "Thiết kế database cho sản phẩm", "Tạo trang danh sách sản phẩm", v.v.

### ❌ Chia sẻ dữ liệu nhạy cảm

- _Sai:_ Dán đoạn code có chứa API Key, mật khẩu thật.

---

## Khung tư duy: Có nên dùng AI cho việc này không?

### Trước khi hỏi AI, hãy check:

1. [ ] Mình có đủ thông tin (ngữ cảnh) để mô tả cho AI không?
2. [ ] Việc này có thể chia nhỏ ra được không?
3. [ ] Có dữ liệu nhạy cảm nào trong prompt không?
4. [ ] Mình có đủ khả năng để đọc và hiểu code AI trả về không?

### Sơ đồ quyết định (Decision Flow)

```
Bạn có một công việc cần làm
    ↓
Có phải code lặp lại/mẫu không? → Đúng → Sử dụng AI ngay! 🟢
    ↓ Sai
Có cần giải thích/học kiến thức? → Đúng → Sử dụng AI để học 🟢
    ↓ Sai
Có phải logic nghiệp vụ mới lạ? → Dùng AI dựng khung, bạn tự viết logic 🟡
    ↓ Sai
Có liên quan bảo mật cực cao? → Tự viết, hoặc dùng AI hỗ trợ rồi review cực kỹ 🔴
```

---

## 🔑 Những điều cần nhớ

1. **Chọn đúng việc cho đúng công cụ** - AI không phải là "vạn năng".
2. **Review là bắt buộc** - Đặc biệt là logic và bảo mật.
3. **Thói quen mới** - Coi AI là một người cộng sự thông minh, hãy học cách thảo luận với nó.

---

**← Bài trước:** [Bài 1: AI Agent là gì?](./lesson-01-what-is-ai-agent.md)
**Bài tiếp theo →** [Module 2: Kỹ năng viết Prompt](../02-basic-prompting/)
