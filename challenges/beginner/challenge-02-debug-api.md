# Thử thách 2: Sửa lỗi cho API (Debug the API)

## 🎯 Mục tiêu

Sử dụng AI để tìm và sửa các lỗi bảo mật cũng như logic trong một đoạn mã nguồn Backend.

## Độ khó: ⭐ Mới bắt đầu

---

## Đoạn code lỗi (Backend Node.js/Express)

```javascript
// routes/users.js
const express = require("express");
const router = express.Router();
const db = require("../db");

// Lấy user theo ID
router.get("/users/:id", async (req, res) => {
  // Lỗi: SQL Injection tiềm ẩn
  const user = await db.query(
    "SELECT * FROM users WHERE id = " + req.params.id
  );
  res.json(user);
});

// Tạo user mới
router.post("/users", async (req, res) => {
  const { name, email, password } = req.body;
  // Lỗi: Lưu mật khẩu dạng plain text
  await db.query(
    `INSERT INTO users (name, email, password) VALUES ('${name}', '${email}', '${password}')`
  );
  res.json({ success: true });
});

module.exports = router;
```

---

## Nhiệm vụ của bạn

Hãy viết prompt yêu cầu AI:

1. Chỉ ra các lỗi bảo mật nghiêm trọng trong đoạn code trên.
2. Sửa lỗi SQL Injection bằng cách dùng **Parameterized Queries**.
3. Sửa lỗi lưu mật khẩu bằng cách dùng thư viện **bcrypt** để hash.
4. Thêm bước **validation** đầu vào cho email (email phải đúng định dạng).

---

## Tiêu chí hoàn thành

- [ ] Không còn lỗi SQL Injection.
- [ ] Mật khẩu được mã hóa trước khi lưu vào DB.
- [ ] Có kiểm tra dữ liệu đầu vào trước khi xử lý.
- [ ] Code có cấu trúc try/catch để tránh crash server.
