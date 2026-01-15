# Thử thách 1: Refactor Code cũ (Legacy Code)

## 🎯 Mục tiêu

Sử dụng AI để biến một đoạn code lộn xộn trở nên sạch sẽ, dễ hiểu và chuyên nghiệp hơn.

## Độ khó: ⭐ Mới bắt đầu

---

## Nội dung thử thách

### Đoạn code ban đầu (Lộn xộn)

```javascript
function calc(a, b, c) {
  if (a == 1) {
    return b + c;
  } else if (a == 2) {
    return b - c;
  } else if (a == 3) {
    return b * c;
  } else if (a == 4) {
    if (c == 0) {
      return "err";
    }
    return b / c;
  } else {
    return 0;
  }
}

function proc(arr) {
  var r = [];
  for (var i = 0; i < arr.length; i++) {
    if (arr[i].x > 0 && arr[i].y > 0) {
      r.push({ a: arr[i].x * 2, b: arr[i].y * 2 });
    }
  }
  return r;
}

function chk(s) {
  if (s.length < 8) return false;
  var h = false,
    n = false;
  for (var i = 0; i < s.length; i++) {
    if (s[i] >= "A" && s[i] <= "Z") h = true;
    if (s[i] >= "0" && s[i] <= "9") n = true;
  }
  return h && n;
}
```

---

## Nhiệm vụ của bạn

Hãy viết các prompt để yêu cầu AI refactor đoạn code trên với các tiêu chí:

1. **Đặt lại tên hàm có ý nghĩa** - Mỗi hàm thực sự làm gì?
2. **Thêm TypeScript types** - Định nghĩa kiểu dữ liệu rõ ràng.
3. **Cú pháp hiện đại** - Sử dụng ES6+ (arrow functions, const/let, map/filter).
4. **Xử lý lỗi chuyên nghiệp** - Không dùng chuỗi trả về kiểu 'err'.
5. **Viết tài liệu** - Thêm chú thích JSDoc.

---

## Tiêu chuẩn hoàn thành

- [ ] Các hàm có tên mô tả đúng chức năng.
- [ ] Có TypeScript interfaces/types đầy đủ.
- [ ] Code ngắn gọn, dễ đọc (dùng logic của ES6).
- [ ] Xử lý lỗi bằng cách throw Error hoặc trả về object có cấu trúc.
- [ ] Có comment giải thích cho các phần khó hiểu.

---

## Gợi ý cho bạn

<details>
<summary>Gợi ý 1: Xác định mục đích các hàm</summary>

- `calc`: Một bộ máy tính (calculator) hỗ trợ cộng, trừ, nhân, chia.
- `proc`: Lọc ra các điểm tọa độ dương và nhân đôi chúng.
- `chk`: Kiểm tra độ mạnh của mật khẩu (độ dài, chữ hoa, số).

</details>

<details>
<summary>Gợi ý 2: Cấu trúc prompt mẫu</summary>

Hãy thử bắt đầu với một hàm trước:

```
"Hãy phân tích và giải thích chức năng của hàm này:
[dán code]

Sau đó, hãy viết lại nó bằng TypeScript với cú pháp hiện đại, đặt tên biến rõ ràng và thêm xử lý lỗi."
```

</details>

<details>
<summary>Gợi ý 3: Riêng cho hàm calc</summary>

Hãy gợi ý AI sử dụng đối tượng (object map) thay vì chuỗi `if-else` dài dặc để code trông sạch hơn.

</details>

---

**Bài tiếp theo →** [Thử thách 2: Debug cho API](./challenge-02-debug-api.md)
