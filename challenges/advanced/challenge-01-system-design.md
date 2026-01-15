# Thử thách 1: Thiết kế hệ thống Collaborative Editor

## 🎯 Mục tiêu

Sử dụng AI để thiết kế kiến trúc cho một ứng dụng chỉnh sửa tài liệu trực tuyến theo thời gian thực (giống Google Docs).

## Độ khó: ⭐⭐⭐ Nâng cao (Advanced)

---

## Bối cảnh bài toán

Bạn cần thiết kế một ứng dụng hỗ trợ:

- Nhiều người cùng sửa một tài liệu cùng lúc.
- Thấy được vị trí con trỏ và lựa chọn của người khác theo thời gian thực.
- Giải quyết xung đột khi hai người sửa cùng một chỗ.
- Lưu trữ lịch sử phiên bản.
- Hỗ trợ tối đa 10,000 người dùng đồng thời trên mỗi tài liệu.

---

## Các yêu cầu cần đáp ứng

### 1. Phía người dùng (Functional)

- Chỉnh sửa đồng thời.
- Xem lịch sử phiên bản và khôi phục.
- Để lại bình luận và gợi ý.
- Chế độ ngoại tuyến (Offline mode) và đồng bộ lại khi có mạng.

### 2. Kỹ thuật (Non-Functional)

- Độ trễ (Latency) < 50ms.
- Độ sẵn sàng (Availability) 99.9%.
- Khả năng mở rộng (Scale) cho 100,000 người dùng toàn hệ thống.

---

## Nhiệm vụ của bạn

Hãy sử dụng AI để thiết kế:

1. **Kiến trúc tổng thể**: Các thành phần chính và cách chúng giao tiếp.
2. **Chiến lược đồng bộ**: Lựa chọn giữa thuật toán OT (Operational Transformation) hay CRDT. Giải thích tại sao.
3. **Thiết kế Database**: Cách lưu trữ tài liệu và các thay đổi (deltas).
4. **Chiến lược mở rộng**: Cách xử lý khi số lượng người dùng tăng đột biến.
5. **Xử lý lỗi**: Điều gì xảy ra khi mất mạng hoặc server bị sập?

---

## Gợi ý các bước đặt câu hỏi (Prompting Tips)

### Mẹo 1: Sử dụng Chain of Thought (Suy luận từng bước)

Đừng hỏi kết quả ngay. Hãy yêu cầu AI phân tích các thách thức trước:

```
"Tôi cần thiết kế một hệ thống collaborative editor giống Google Docs.
Trước khi đưa ra kiến trúc chi tiết, hãy phân tích:
1. Những thách thức lớn nhất của việc đồng bộ thời gian thực là gì?
2. So sánh OT và CRDT trong bối cảnh này.
..."
```

### Mẹo 2: Yêu cầu sơ đồ

Yêu cầu AI cung cấp sơ đồ bằng định dạng Mermaid để bạn có thể hình dung dễ dàng.

---

## Tiêu chuẩn đánh giá

- [ ] Sự tách biệt rõ ràng giữa các service.
- [ ] Giải quyết được vấn đề xung đột dữ liệu.
- [ ] Có phương án cho việc xử lý độ trễ.
- [ ] Database được thiết kế phù hợp cho việc lưu lịch sử.

---

**← Xem thêm:** [Thử thách trung cấp](../intermediate/)
