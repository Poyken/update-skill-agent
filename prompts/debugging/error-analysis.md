# Prompt mẫu để Phân tích lỗi (Error Analysis)

## 1. Điều tra lỗi cụ thể

```
Tôi đang gặp lỗi sau:
[Dán toàn bộ thông báo lỗi ở đây]

Ngữ cảnh (Context):
- File: [tên file]
- Dòng: [số dòng nếu có]
- Hành động: [bạn đang làm gì thì lỗi xảy ra]
- Thay đổi gần nhất: [bạn vừa sửa gì trước khi lỗi]

Đoạn code liên quan:
[Dán code ở đây]

Hãy giúp tôi:
1. Giải thích nguyên nhân gây ra lỗi này.
2. Cách sửa lỗi.
3. Cách phòng tránh lỗi tương tự trong tương lai.
```

---

## 2. Lỗi Build hoặc Compile

```
Quá trình Build/Compile thất bại với lỗi:
[Dán lỗi build ở đây]

Môi trường:
- Phiên bản Node/Language: [phiên bản]
- Trình quản lý gói: [npm/yarn/pnpm]
- Framework: [tên framework + phiên bản]

Các phụ thuộc (Dependencies) liên quan trong package.json:
[Dán phần dependencies liên quan]

Nguyên nhân có thể là gì và cách khắc phục như thế nào?
```

---

## 3. Lỗi Ứng dụng bị Crash (Runtime)

```
Ứng dụng bị dừng đột ngột (Crash) với log sau:
[Dán crash log/stack trace]

Các bước tái hiện lỗi:
1. [bước 1]
2. [bước 2]
3. [crash xảy ra]

Sự cố này bắt đầu sau khi tôi: [thay đổi gần nhất]
```

---

## 4. Phân tích Hiệu suất (Performance)

```
Gặp vấn đề về hiệu suất trong [component/hàm]:

Triệu chứng:
- [mô tả tình trạng chậm/lag]
- [xảy ra khi nào]

Code hiện tại:
[Dán đoạn code nghi ngờ gây chậm]

Hãy phân tích các điểm nghẽn (bottlenecks) và đề xuất cách tối ưu hóa.
```
