# 📦 Pre-built Templates cho các Tech Stacks phổ biến

> Folder này chứa các `.agent` templates sẵn sàng sử dụng cho các tech stacks phổ biến.

---

## 📋 Danh sách Templates

| Stack                     | File                                       | Best for                   |
| ------------------------- | ------------------------------------------ | -------------------------- |
| **Next.js + TailwindCSS** | [nextjs-tailwind.md](./nextjs-tailwind.md) | Modern React apps, SSR/SSG |
| **NestJS + Prisma**       | [nestjs-prisma.md](./nestjs-prisma.md)     | Enterprise backends        |
| **React + Vite**          | [react-vite.md](./react-vite.md)           | SPAs, dashboards           |
| **Express + MongoDB**     | [express-mongodb.md](./express-mongodb.md) | Simple APIs                |

---

## 🚀 Cách sử dụng

### Bước 1: Copy template phù hợp

```bash
# Ví dụ cho Next.js project
cp prebuilt-templates/nextjs-tailwind.md .agent/TEMPLATE.md
```

### Bước 2: Customize cho dự án của bạn

```
Đã paste template từ prebuilt-templates/nextjs-tailwind.md

Hãy đọc template này và CUSTOMIZE cho dự án hiện tại:
1. Thay [Project Name] bằng tên thật
2. Quét codebase để update Tech Stack chính xác
3. Thay các ví dụ placeholder bằng code thực tế từ src/
4. Cập nhật trạng thái features

Output: Các files .agent/ đã customized
```

### Bước 3: Validate

Chạy validation theo hướng dẫn tại [validation-checklist.md](../validation-checklist.md)

---

## 📝 Template Format

Mỗi template file chứa:

```markdown
# [Stack Name] Template

## Files sẽ được tạo

- .agent/memory/project-context.md
- .agent/rules/global.md
- .agent/rules/[domain].md
- .agent/workflows/create-new-feature.md
- .agent/checklists/pr-review.md

## Template Content

### FILE: .agent/memory/project-context.md

[content]

### FILE: .agent/rules/global.md

[content]

...
```

---

## ➕ Đóng góp Template mới

Nếu bạn đã setup `.agent` cho một stack khác và muốn share:

1. Tổng hợp các files trong `.agent/` thành 1 file theo format trên
2. Thay các thông tin cụ thể bằng `[PLACEHOLDER]`
3. Thêm vào thư mục này
4. Update README

---

**← Quay lại:** [Hướng dẫn vận hành](../operation-guide.md)
