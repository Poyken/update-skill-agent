# Prompt mẫu để tạo Code (Code Generation)

## 1. Tạo Hàm (Function Generation)

```
Viết một hàm [tênHàm] thực hiện:

Đầu vào (Input):
- [thamSố1]: [kiểu dữ liệu] - [mô tả]
- [thamSố2]: [kiểu dữ liệu] - [mô tả]

Đầu ra (Output):
- [kiểu dữ liệu trả về] - [mô tả]

Logic xử lý:
1. [bước 1]
2. [bước 2]
3. [bước 3]

Các trường hợp biên cần xử lý (Edge cases):
- [trường hợp 1]
- [trường hợp 2]

Ngôn ngữ: [tên ngôn ngữ sử dụng]
```

### Ví dụ:

```
Viết một hàm formatCurrency thực hiện:

Đầu vào (Input):
- amount: number - Giá trị số cần định dạng
- currency: string - Mã tiền tệ (USD, VND, EUR)
- locale: string - Tùy chọn, mặc định là 'vi-VN'

Logic xử lý:
1. Kiểm tra amount có phải là số hợp lệ không
2. Định dạng số theo chuẩn tiền tệ của locale tương ứng
3. Trả về chuỗi đã định dạng

Các trường hợp biên:
- Nếu amount là NaN hoặc undefined → trả về "0"
- Hỗ trợ số âm

Ngôn ngữ: TypeScript
```

---

## 2. Tạo Lớp (Class Generation)

```
Tạo một [class/module] cho mục đích [mô tả mục đích]:

Thuộc tính (Properties):
- [thuộcTính1]: [kiểu dữ liệu] - [phạm vi truy cập: private/public]
- [thuộcTính2]: [kiểu dữ liệu]

Phương thức (Methods):
- [phươngThức1]([params]): [kiểu trả về]
- [phươngThức2]([params]): [kiểu trả về]

Thiết kế: [Design Pattern nếu có]
Phụ thuộc (Dependencies): [các thư viện/service bên ngoài cần dùng]
```

---

## 3. Tạo các hàm tiện ích (Utility Functions)

```
Tạo bộ các hàm tiện ích (utilities) cho [lĩnh vực, ví dụ: xử lý chuỗi]:

Các hàm cần có:
1. [tên hàm 1] - [mục đích]
2. [tên hàm 2] - [mục đích]

Yêu cầu:
- Là các hàm thuần túy (pure functions)
- Sử dụng TypeScript với kiểu dữ liệu chặt chẽ
- Có chú thích JSDoc cho từng hàm
- Handle các trường hợp dữ liệu rỗng hoặc null
```

---

## 4. Viết Thuật toán (Algorithm Implementation)

```
Triển khai thuật toán [tên thuật toán]:

Bài toán:
[Mô tả bài toán]

Đầu vào: [định dạng dữ liệu vào]
Đầu ra: [định dạng dữ liệu ra]

Ràng buộc (Constraints):
- Độ phức tạp thời gian: O([?])
- Độ phức tạp không gian: O([?])

Yêu cầu: Giải thích chi tiết các bước thực hiện trong comment.
```
