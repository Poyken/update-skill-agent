# Bài 1: Kỹ thuật Chain of Thought (Suy luận từng bước)

## 🎯 Mục tiêu bài học

- Hiểu kỹ thuật Chain of Thought (CoT) là gì.
- Biết khi nào nên dùng CoT để giải quyết các bài toán phức tạp.
- Áp dụng CoT để nhận diện tư duy của AI.

---

## Chain of Thought (Chuỗi suy nghĩ) là gì?

Chain of Thought là kỹ thuật yêu cầu AI **"suy nghĩ từng bước một"** trước khi đưa ra kết luận hoặc code cuối cùng.

### Tại sao kỹ thuật này hiệu quả?

- Buộc AI phải chia nhỏ vấn đề.
- Giảm thiểu sai sót trong các lập luận logic phức tạp.
- Giúp bạn thấy được tư duy của AI, từ đó dễ dàng phát hiện ra các giả định sai.

---

## Khi nào nên sử dụng CoT?

### ✅ Nên dùng khi:

- **Thuật toán phức tạp**: Các logic có nhiều bước tính toán.
- **Quyết định kiến trúc**: Khi cần so sánh các lựa chọn đánh đổi.
- **Sửa lỗi khó (Deep Debugging)**: Khi cần phân tích nguyên nhân gốc rễ.
- **Tối ưu hóa hiệu suất**: Khi cần xác định các điểm nghẽn.
- **Phân tích bảo mật**: Khi cần rà soát các lỗ hổng tiềm ẩn.

### ❌ Không cần dùng khi:

- Viết các hàm đơn giản.
- Tạo code boilerplate (mẫu).
- Định dạng lại code (formatting).
- Hỏi về cú pháp ngôn ngữ.

---

## Các mẫu câu lệnh CoT (CoT Templates)

### Mẫu 1: Phân tích trước khi làm

```
Trước khi triển khai [tên task], hãy:
1. Phân tích các yêu cầu đầu vào.
2. Xác định các thách thức tiềm ẩn.
3. Đề xuất 2-3 hướng tiếp cận khác nhau.
4. Đánh giá ưu/nhược điểm từng hướng.
5. Chọn hướng tốt nhất và giải thích lý do.
6. Sau đó mới bắt đầu viết code.
```

### Mẫu 2: Suy luận Debugging

```
Tôi gặp lỗi sau trong code: [dán code và lỗi]

Trước khi đưa ra cách sửa, hãy:
1. Giải thích dòng code này đang cố gắng làm gì.
2. Truy vết (trace) quá trình thực thi từ đầu đến cuối.
3. Xác định chính xác vị trí logic bị sai.
4. Giải thích tại sao nó sai.
5. Cuối cùng mới đưa ra mã nguồn đã sửa.
```

---

## Ví dụ thực tế

### ❌ Không dùng CoT

> **Prompt:** "API của tôi chạy chậm, hãy tối ưu nó."
> **Response:** [AI nhảy ngay vào đề xuất các cách tối ưu ngẫu nhiên mà không hiểu thực tế hệ thống bạn ra sao].

### ✅ Có dùng CoT

> **Prompt:** "Endpoint GET /api/products đang chạy chậm (mất 2 giây).
>
> Trước khi tối ưu, hãy:
>
> 1. Phân tích các nguyên nhân phổ biến có thể gây chậm API.
> 2. Xem code của tôi bên dưới và chỉ ra các điểm nghẽn.
> 3. Xếp hạng các cách tối ưu theo tiêu chí: Ảnh hưởng cao - Tốn ít công sức.
> 4. Triển khai các thay đổi ưu tiên nhất.
>
> Code của tôi: [dán code]"

---

## 📝 Bài tập thực hành

### Bài tập 1: Áp dụng CoT

Hãy viết một prompt sử dụng CoT cho yêu cầu: "Thiết lập giới hạn số lần gọi API (Rate limiting) cho server Node.js".

### Bài tập 2: So sánh kết quả

Chọn một bài toán thuật toán (ví dụ: tìm đường đi ngắn nhất).

1. Thử prompt thẳng vào vấn đề.
2. Thử prompt dùng CoT.
   Quan sát xem cách nào cho kết quả chính xác và ít bug hơn.

---

## 🔑 Những điều cần nhớ

1. **CoT = Suy nghĩ trước, hành động sau.**
2. **Logic minh bạch** giúp bạn kiểm soát AI tốt hơn.
3. **Chất lượng hơn số lượng**: Một prompt CoT có thể dài hơn nhưng tiết kiệm cho bạn hàng giờ debug sau này.

---

**Bài tiếp theo →** [Bài 2: Cải thiện lặp lại (Iterative Refinement)](./lesson-02-iterative-refinement.md)
