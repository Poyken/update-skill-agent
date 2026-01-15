# Hướng dẫn thiết lập thư mục `.agent` cho Dự án hiện có

## 🎯 Mục đích

Thư mục `.agent` (hoặc `.cursor`, `.github/copilot` tùy tool) đóng vai trò như **"Bộ nhớ dài hạn"** của AI về dự án của bạn. Thay vì phải mô tả lại toàn bộ context mỗi lần chat, AI sẽ tự động đọc các file trong thư mục này để hiểu:

1. **Kiến trúc tổng thể** của dự án.
2. **Quy chuẩn code** (Coding conventions) bạn đang dùng.
3. **Các quy trình làm việc (Workflows)** thường xuyên.
4. **Những gì đã hoàn thành** và **những gì còn lại**.

---

## 🚀 Bắt đầu nhanh

### 📖 Tài liệu chính

| Tài liệu                                                   | Mô tả                                   |
| ---------------------------------------------------------- | --------------------------------------- |
| 👉 **[Hướng dẫn vận hành](./operation-guide.md)**          | Quy trình 5 bước đầy đủ với checkpoints |
| 📝 **[Bộ Prompts đầy đủ](./prompts-to-generate-agent.md)** | 40+ prompts sẵn dùng                    |
| ✅ **[Validation Checklist](./validation-checklist.md)**   | Kiểm tra .agent đã đúng chưa            |
| 📊 **[Success Metrics](./success-metrics.md)**             | Đo lường hiệu quả của .agent            |
| ⚙️ **[Tool-Specific Configs](./tool-specific-configs.md)** | Cấu hình cho Cursor/Copilot/Claude      |

### 📦 Pre-built Templates

Muốn bắt đầu ngay? Dùng template có sẵn:

| Stack                     | Template                                                      |
| ------------------------- | ------------------------------------------------------------- |
| **Next.js + TailwindCSS** | [nextjs-tailwind.md](./prebuilt-templates/nextjs-tailwind.md) |
| **NestJS + Prisma**       | [nestjs-prisma.md](./prebuilt-templates/nestjs-prisma.md)     |

### 📋 Templates cơ bản

- [project-context.template.md](./project-context.template.md) - Mẫu mô tả dự án
- [conventions.template.md](./conventions.template.md) - Mẫu quy chuẩn code
- [progress.template.md](./progress.template.md) - Mẫu theo dõi tiến độ

### 📘 Ví dụ thực tế

- [example-backend-api.md](./example-backend-api.md) - Ví dụ cho Backend API
- [example-frontend-web.md](./example-frontend-web.md) - Ví dụ cho Frontend Web

## 📁 Cấu trúc thư mục `.agent` NÂNG CAO

```
your-project/
├── .agent/
│   ├── rules/                    # 📜 Quy tắc code (RÚT TỪ CODE THẬT)
│   │   ├── global.md             # Quy tắc chung toàn dự án
│   │   ├── ui-components.md      # Quy tắc riêng cho UI
│   │   ├── state-management.md   # Quy tắc quản lý state
│   │   └── api-integration.md    # Quy tắc gọi API
│   │
│   ├── checklists/               # ✅ Danh sách kiểm tra
│   │   ├── pr-review.md          # Review pull request
│   │   ├── feature-deployment.md # Deploy tính năng mới
│   │   └── [domain-specific].md  # Checklist cho logic cốt lõi
│   │
│   ├── workflows/                # 🔄 Quy trình tự động
│   │   ├── create-new-feature.md # Tạo feature mới
│   │   └── fix-bug-flow.md       # Quy trình sửa bug
│   │
│   ├── templates/                # 📦 Mẫu code
│   │   └── component.template.md # Template cho component chính
│   │
│   ├── skills/                   # 🧠 Kỹ năng tư duy cho AI
│   │   ├── review-skill.md       # Cách review code
│   │   ├── debug-skill.md        # Cách debug hiệu quả
│   │   └── performance-skill.md  # Tối ưu hiệu suất
│   │
│   ├── docs/                     # 📚 Kiến thức dự án
│   │   └── architecture.md       # Kiến trúc hệ thống
│   │
│   ├── memory/                   # 🧠 Bộ nhớ dài hạn
│   │   └── project-context.md    # Trạng thái + lỗi đã fix
│   │
│   └── mocks/                    # 🎭 Dữ liệu giả
│       └── sample-data.json      # Mock data cho test/UI
│
└── ... (các file code của dự án)
```

### Giải thích các thư mục:

| Folder        | Mục đích                           | Khi nào cần            |
| ------------- | ---------------------------------- | ---------------------- |
| `rules/`      | Quy tắc code RÚT TỪ CODE THẬT      | Luôn cần               |
| `checklists/` | Danh sách kiểm tra trước PR/Deploy | Cần cho team > 1 người |
| `workflows/`  | Quy trình làm việc lặp lại         | Luôn cần               |
| `templates/`  | Mẫu code để AI copy                | Rất hữu ích            |
| `skills/`     | "Dạy" AI cách tư duy               | Nâng cao               |
| `docs/`       | Kiến thức đặc thù dự án            | Dự án phức tạp         |
| `memory/`     | Lưu context giữa các sessions      | Luôn cần               |
| `mocks/`      | Dữ liệu giả cho test/UI            | Khi viết tests         |

---

## 📝 Nội dung từng file

### 1. `project-context.md` (BẮT BUỘC - File quan trọng nhất)

Đây là file AI sẽ đọc đầu tiên để hiểu "bức tranh toàn cảnh" về dự án.

```markdown
# [Tên Dự Án]

## Mô tả ngắn gọn

[1-2 câu mô tả dự án làm gì, cho ai]

## Tech Stack

- **Frontend:** [React 18, Next.js 14, TailwindCSS...]
- **Backend:** [Node.js, Express, NestJS...]
- **Database:** [PostgreSQL, MongoDB, Prisma ORM...]
- **Infra/Deploy:** [Docker, AWS, Vercel...]
- **Testing:** [Jest, Playwright...]

## Cấu trúc thư mục chính

- `src/components/` - Các UI components tái sử dụng
- `src/features/` - Logic theo từng tính năng (Feature-based)
- `src/services/` - Các hàm gọi API
- `src/hooks/` - Custom React hooks
- `src/utils/` - Hàm tiện ích dùng chung
- `prisma/` - Database schema và migrations

## Trạng thái hiện tại

- [x] Authentication (Hoàn thành)
- [x] User Management (Hoàn thành)
- [/] Product Catalog (Đang làm - 70%)
- [ ] Payment Integration (Chưa bắt đầu)
- [ ] Admin Dashboard (Chưa bắt đầu)

## Lưu ý quan trọng khi làm việc

- Luôn dùng TypeScript strict mode.
- Mọi API call phải đi qua service layer (`src/services/`).
- Không commit trực tiếp vào `main`, tạo branch feature.
```

---

### 2. `architecture.md` (Tùy chọn - Dự án phức tạp)

Mô tả chi tiết hơn về kiến trúc, phù hợp cho dự án lớn hoặc microservices.

```markdown
# Kiến trúc Hệ thống

## Sơ đồ tổng quan

[Có thể dùng Mermaid diagram ở đây]

## Flow dữ liệu chính

1. User request → API Gateway
2. Gateway → Auth middleware
3. Authenticated → Service Layer → Database
4. Response → Transformed → Client

## Các Service chính

- **AuthService:** Xử lý đăng nhập, token, phân quyền.
- **ProductService:** CRUD sản phẩm, inventory.
- **OrderService:** Quản lý đơn hàng, thanh toán.

## Database Schema

[Link đến file schema hoặc mô tả các bảng chính]
```

---

### 3. `conventions.md` (Khuyến nghị)

Giúp AI viết code đúng phong cách của dự án bạn.

```markdown
# Quy chuẩn Code

## Naming Conventions

- **Components:** PascalCase (ví dụ: `UserProfile.tsx`)
- **Hooks:** camelCase bắt đầu bằng `use` (ví dụ: `useAuth.ts`)
- **Utils:** camelCase (ví dụ: `formatDate.ts`)
- **Constants:** UPPER_SNAKE_CASE (ví dụ: `API_BASE_URL`)

## File Structure cho Component

Mỗi component phức tạp nên có cấu trúc:
```

ComponentName/
├── index.tsx # Logic chính
├── ComponentName.styles.ts # Styles (nếu dùng CSS-in-JS)
├── ComponentName.test.tsx # Unit tests
└── types.ts # TypeScript interfaces

```

## Quy tắc Git
- Branch naming: `feature/ten-tinh-nang`, `fix/ten-bug`
- Commit message: Dùng Conventional Commits (feat:, fix:, refactor:)

## Error Handling
- Mọi API call phải wrap trong try-catch.
- Dùng custom `AppError` class cho business errors.
- Log errors bằng service logging (không dùng console.log trong production).
```

---

### 4. `progress.md` (Khuyến nghị - Cập nhật thường xuyên)

Giúp AI biết việc gì đã xong, việc gì đang làm dở, việc gì còn lại.

```markdown
# Tiến độ Dự án

## Sprint hiện tại: Sprint 5 (01/01 - 15/01)

### Đang thực hiện (In Progress)

- [ ] Tích hợp Stripe Payment Gateway
  - [x] Setup Stripe SDK
  - [ ] Tạo checkout session
  - [ ] Webhook xử lý thanh toán thành công

### Đã hoàn thành gần đây

- [x] Refactor ProductService sang Repository pattern
- [x] Thêm unit tests cho AuthService (coverage 85%)

### Backlog (Chưa bắt đầu)

- [ ] Admin Dashboard
- [ ] Export báo cáo PDF
- [ ] Push notification
```

---

### 5. `workflows/` (Tùy chọn - Rất hữu ích)

Các hướng dẫn từng bước cho những tác vụ AI sẽ thực hiện lặp đi lặp lại.

#### `workflows/add-new-feature.md`

```markdown
# Quy trình thêm tính năng mới

1. Tạo branch mới từ `develop`: `git checkout -b feature/ten-tinh-nang`
2. Tạo folder trong `src/features/[ten-tinh-nang]/`
3. Định nghĩa types trong `types.ts`
4. Viết service layer trong `src/services/`
5. Tạo components UI
6. Viết unit tests (coverage tối thiểu 70%)
7. Tạo Pull Request vào `develop`
```

#### `workflows/fix-bug.md`

```markdown
# Quy trình sửa bug

1. Tái hiện lỗi và ghi lại các bước.
2. Viết test case fail để reproduce bug.
3. Sửa code.
4. Đảm bảo test case pass.
5. Chạy lại toàn bộ test suite: `npm test`
6. Commit với message: `fix: mô-tả-ngắn-gọn`
```

---

## 🚀 Prompt mẫu để yêu cầu AI tạo thư mục `.agent`

Khi bạn đã có một dự án hiện có, hãy dùng prompt sau để yêu cầu AI giúp bạn tạo cấu trúc `.agent`:

```
Dự án của tôi đã hoàn thành khoảng 80%. Hãy giúp tôi tạo thư mục .agent/ để AI có thể hiểu và hỗ trợ phát triển tiếp.

Thông tin dự án:
- Tên: [Tên dự án]
- Mục đích: [Mô tả ngắn]
- Tech Stack: [Frontend, Backend, DB...]
- Cấu trúc thư mục hiện tại: [Liệt kê các folder chính]

Những gì đã hoàn thành:
- [Tính năng 1]
- [Tính năng 2]

Những gì đang làm dở:
- [Tính năng 3 - đang làm]

Những gì chưa bắt đầu:
- [Tính năng 4]
- [Tính năng 5]

Quy chuẩn code đặc biệt (nếu có):
- [Ví dụ: Dùng Functional Components, không dùng Class]

Hãy tạo các file sau trong thư mục .agent/:
1. project-context.md
2. conventions.md
3. progress.md
```

---

## 💡 Mẹo sử dụng hiệu quả

1. **Cập nhật `progress.md` thường xuyên:** Mỗi khi hoàn thành một task, hãy cập nhật file này. AI sẽ luôn biết trạng thái mới nhất.

2. **Đừng viết quá chi tiết:** File context nên ngắn gọn, súc tích. AI không cần biết mọi thứ, chỉ cần biết đủ để làm việc.

3. **Dùng liên kết:** Thay vì copy-paste code, dùng đường dẫn file. Ví dụ: "Xem schema tại `prisma/schema.prisma`".

4. **Tạo workflows cho tác vụ lặp:** Nếu bạn thường xuyên làm một việc (thêm API, tạo component), hãy viết một workflow và AI sẽ làm theo đúng quy trình của bạn.
