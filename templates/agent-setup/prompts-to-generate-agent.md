# Prompt Mẫu để AI tự động tạo thư mục `.agent` HOÀN CHỈNH

Bộ prompts này được thiết kế để AI có thể **quét codebase hiện có** và **tự động sinh ra cấu trúc `.agent/` đầy đủ** - bao gồm rules, checklists, workflows, templates, skills, docs, memory và mocks.

---

> 📖 **Trước khi bắt đầu:** Đọc [Hướng dẫn vận hành](./operation-guide.md) để biết cách sử dụng bộ prompts này hiệu quả nhất.

---

## 📁 Cấu trúc `.agent` Nâng cao

```
.agent/
├── rules/                    # Quy tắc code (Quan trọng nhất)
│   ├── global.md             # Quy tắc chung toàn dự án
│   ├── ui-components.md      # Quy tắc riêng cho UI
│   ├── state-management.md   # Quy tắc quản lý state
│   └── api-integration.md    # Quy tắc gọi API
├── checklists/               # Danh sách kiểm tra
│   ├── pr-review.md          # Review pull request
│   ├── feature-deployment.md # Deploy tính năng mới
│   └── [domain-specific].md  # Checklist cho logic cốt lõi
├── workflows/                # Quy trình tự động
│   ├── create-new-feature.md # Tạo feature mới
│   └── fix-bug-flow.md       # Quy trình sửa bug
├── templates/                # Mẫu code
│   └── component.template.md # Template cho component chính
├── skills/                   # Kỹ năng tư duy cho AI
│   ├── review-skill.md       # Cách review code
│   ├── debug-skill.md        # Cách debug hiệu quả
│   └── performance-skill.md  # Tối ưu hiệu suất
├── docs/                     # Kiến thức dự án
│   └── architecture.md       # Kiến trúc hệ thống
├── memory/                   # Bộ nhớ dài hạn
│   └── project-context.md    # Trạng thái hiện tại + lỗi đã fix
└── mocks/                    # Dữ liệu giả
    └── sample-data.json      # Mock data cho test/UI
```

---

# 📜 PHẦN 1: RULES (Quy tắc Code)

> **📏 QUY TẮC CHUNG CHO TẤT CẢ PROMPTS:**
>
> ❌ **KHÔNG ĐƯỢC viết:**
>
> - "should", "best practice", "recommended", "ideally"
> - Lý thuyết chung không có evidence từ code
> - Rules copy từ documentation của thư viện
>
> ✅ **BẮT BUỘC phải có:**
>
> - Evidence file: `src/path/to/file.ts`
> - Code example thực tế từ codebase
> - Nếu không tìm thấy → ghi `[KHÔNG TÌM THẤY - CẦN XÁC NHẬN]`

---

## Prompt 1.1: Tạo `rules/global.md` - Quy tắc cấp độ Hệ thống

**⏱️ Thời gian:** 10-15 phút | **📄 Target:** 80-120 dòng | **📊 Sections:** 6-8

```markdown
Bạn là một Senior Developer. Hãy quét TOÀN BỘ codebase để rút ra các quy tắc code đang được thực thi trên thực tế (De-facto standards) để tạo file `.agent/rules/global.md`.

**YÊU CẦU PHÂN TÍCH (Cấm viết lý thuyết):**

1. **Naming Strategy (Dựa trên 20+ file ngẫu nhiên):**

   - Pattern đặt tên: Files, Components, Functions, Variables, Constants, Types.
   - Folder naming: kebab-case, camelCase hay PascalCase?

2. **File & Folder Anatomy:**

   - Cấu trúc 1 module chuẩn: Gồm những file nào? (vd: controller, service, rpc, style, test).
   - Vị trí file test: Cạnh source hay folder tập trung?

3. **TypeScript & Type System:**

   - Search: "any", "as any", "unknown". Rút ra quy tắc về tính nghiêm ngặt.
   - Ưu tiên: Interface vs Type? Enum vs Const Object?

4. **Import/Export Conventions:**

   - Phân tích 10 file: Thứ tự import (library -> internal -> styles)?
   - Xuất: Default export hay Named export? Pattern dùng barrel files (index.ts).

5. **Error & Exception Handling:**

   - Pattern try-catch: Ở tầng nào? Có dùng Custom Error class không?
   - Logging: Dùng console.log hay library? Pattern log data.

6. **Git/Commit Standards:**
   - Đọc 10 commit gần nhất: Pattern là gì? (Conventional Commits, Prefix-based?).

**BẮT BUỘC TRONG OUTPUT (Mỗi mục):**

- **Pattern:** [Mô tả chi tiết quy tắc tìm thấy]
- **Evidence:** `path/to/evidence/file.ts`
- **Code Snippet:** [1 đoạn code thực tế minh họa quy tắc này]

Nếu không tìm thấy pattern rõ ràng, ghi: `[KHÔNG TÌM THẤY - CẦN USER XÁC NHẬN]`.
```

**Output Format (BẮT BUỘC theo format này):**

````markdown
# Quy tắc Code Chung - [Tên Dự Án]

> ⚠️ Các quy tắc này được rút ra từ code hiện có, KHÔNG phải lý thuyết.

## 1. Naming Conventions

| Loại       | Pattern         | Evidence File                 |
| ---------- | --------------- | ----------------------------- |
| Components | PascalCase      | `src/components/UserCard.tsx` |
| Hooks      | camelCase + use | `src/hooks/useAuth.ts`        |

**Ví dụ code thực tế:**

```tsx
// Từ src/components/UserCard.tsx
export function UserCard({ user }: UserCardProps) { ... }
```
````

## 2. File Organization

[Tương tự với evidence + example]

...

`````

---

## Prompt 1.2: Tạo `rules/ui-components.md` - Quy tắc UI & UX

**⏱️ Thời gian:** 8-10 phút | **📄 Target:** 60-90 dòng | **📊 Sections:** 5-7

````markdown
Phân tích sâu folder `src/components/` và `src/pages/` để tạo file `.agent/rules/ui-components.md`. Tập trung vào tính đồng nhất giao diện và trải nghiệm.

**YÊU CẦU PHÂN TÍCH (Dựa trên 10 components phức tạp nhất):**

1. **Component Design System:**
   - Cách handle Props: Inline types, Separated types, hay Generic props?
   - Có dùng HOCs, Render Props hay Composition?

2. **Styling & Rich Aesthetics (QUAN TRỌNG):**
   - Tailwind/CSS Modules/Styled: Cách đặt tên classes, cách dùng Design Tokens (màu sắc, spacing).
   - Hover/Active/Focus states: Patterns chung là gì?
   - Có dùng Gradients, Shadows, hay Animations không? (Mô tả pattern).

3. **Interactions & States:**
   - Quản lý Local State: useState vs useReducer?
   - Handle Loading/Empty/Error states: Pattern UI chung (Skeletons, Spinners?).

4. **Accessibility (A11y) & SEO:**
   - Kiểm tra `aria-` labels, `alt` text, heading hierarchy.
   - Semantic HTML: Dùng `section`, `article`, `main` hay chỉ `div`?

5. **Design Patterns UI:**
   - Cách viết Wrapper components (vd: Layout, Container).
   - Pattern xử lý Conditional Rendering (&& vs ternary vs Early return).

**BẮT BUỘC:**
- Chỉ ghi những gì **BẠN THẤY THỰC TẾ**.
- Mỗi quy tắc phải có **Evidence File** và **Code Snippet**.
- Nếu dự án dùng Tailwind, bắt buộc liệt kê các `custom base classes` tìm thấy.
`````

---

## Prompt 1.3: Tạo `rules/state-management.md` - Quản lý Dữ liệu

**⏱️ Thời gian:** 10 phút | **📄 Target:** 50-80 dòng

```markdown
Hãy phân tích cách dự án quản lý dữ liệu (State) từ Client đến Server để tạo `.agent/rules/state-management.md`.

**NỘI DUNG CẦN TRÍCH XUẤT:**

1. **Global State Strategy:**

   - Library: Redux (Slice pattern?), Zustand (Store pattern?), Context?
   - Naming: Actions, Selectors, Stores (vd: `useUserStore` vs `userStore`).

2. **Server State (Remote Data):**

   - Tool: React Query, SWR, Apollo.
   - Pattern: Có dùng custom hooks cho API gọi không? (vd: `useFetchUsers`).
   - Caching: Quy tắc `staleTime`, `cacheTime`, `retry` đang được set mặc định là bao nhiêu?

3. **Persistence & Sync:**

   - Có lưu state vào LocalStorage/Cookies không? Pattern xử lý là gì?
   - Cách sync giữa các tabs hoặc các trang.

4. **Logical Separation:**
   - Tỷ lệ dùng Global state vs Local state. Khi nào dev dự án này chọn Global state?

**BẮT BUỘC:** Cung cấp Evidence cho từng công nghệ được nhắc tên. Nếu không dùng Library nào, hãy mô tả pattern Context/State truyền thống tìm thấy.
```

---

# ✅ PHẦN 2: CHECKLISTS

## Prompt 2.1: Tạo `checklists/pr-review.md` - Bộ lọc chất lượng

```markdown
Hãy tạo một checklist review code cực kỳ nghiêm ngặt tại `.agent/checklists/pr-review.md`. Checklist này phải được xây dựng DỰA TRÊN các rules đã tìm thấy ở `global.md`.

**CẤU TRÚC PHÂN LOẠI (Bắt buộc):**

1. **🚨 CRITICAL (Chặn Merge):**

   - Security: Hardcode secrets, SQL Injection, XSS.
   - Logic: Race conditions, memory leaks, data loss.
   - Conventions: Sai cấu trúc thư mục, sai naming core.

2. **⚠️ MAJOR (Cần sửa):**

   - Performance: Re-render không cần thiết, loop API calls.
   - TypeScript: Dùng `any` bừa bãi, thiếu types cho props.
   - Styling: Dùng màu/font lạ không có trong Design System.

3. **📝 MINOR (Nhắc nhở):**
   - Clean Code: Folder quá 3 cấp, function quá 50 dòng.
   - Documentation: Thiếu JSDoc cho hàm phức tạp, thiếu README cho module mới.

**YÊU CẦU:** Mỗi đầu mục checklist phải đi kèm mô tả ngắn "Tại sao" (Lấy bài học từ chính codebase này).
```

---

## Prompt 2.2: Tạo `checklists/feature-deployment.md` - Checkliste Vận hành

```markdown
Bạn là một DevOps Engineer. Hãy đọc các file cấu hình (`package.json`, `github/workflows`, `docker-compose.yml`, `ecosystem.config.js`, `.env`) để tạo checklist deploy tại `.agent/checklists/feature-deployment.md`.

**NỘI DUNG CẦN CÓ:**

1. **Pre-build:** `npm run lint`, `npm run test`, `check env variables`.
2. **Build & Build Verification:** Cách verify build artifact thành công.
3. **Database Migration:** Lệnh chạy migration, lệnh rollback nếu lỗi.
4. **Environment Check:** Danh sách các ENV bắt buộc phải có cho feature mới.
5. **Post-deploy:** Smoke test commands, log monitoring commands.

**YÊU CẦU:** Chèn các LỆNH TERMINAL THỰC TẾ từ dự án vào checklist.
```

---

## Prompt 2.3: Tạo Checklist cho Logic Cốt lõi (Domain-specific)

```

Xác định LOGIC CỐT LÕI của dự án và tạo checklist riêng cho nó.

**Bước 1: Xác định domain chính**

- Đọc README, package.json description
- Tìm folder/module lớn nhất, phức tạp nhất
- Xác định các keywords: pose-tracking, camera, authentication, payment...

**Bước 2: Phân tích logic cốt lõi**

- Tìm các files chính của domain đó
- Xác định các edge cases quan trọng
- Tìm các TODO/FIXME liên quan

**Bước 3: Tạo checklist**
Ví dụ nếu là Pose Tracking:

- [ ] Camera permissions được handle đúng
- [ ] Fallback khi không có camera
- [ ] Performance: FPS không drop dưới 30
- [ ] Memory leaks từ video stream

**Output:** File `checklists/[domain-name].md` với checklist chuyên sâu.

```

---

# 🔄 PHẦN 3: WORKFLOWS

## Prompt 3.1: Tạo `workflows/create-new-feature.md` - Quy trình chuẩn

**⏱️ Thời gian:** 8-10 phút

```markdown
Bạn hãy đóng vai trò là Tech Lead. Phân tích module hoàn thiện nhất trong dự án (ví dụ `src/features/X` hoặc `src/modules/Y`) để tạo workflow tạo tính năng mới tại `.agent/workflows/create-new-feature.md`.

**CÁC BƯỚC PHÂN TÍCH:**

1. Liệt kê chính xác cấu trúc folder + file của module mẫu.
2. Identiy "Core Skeleton" của module đó.
3. Xác định các điểm tích hợp (vd: phải đăng ký ở app.module.ts, thêm route ở router.tsx).

**NỘI TRÌNH TRONG FILE:**

1. **Step 1: Scaffolding** (Lệnh terminal hoặc cấu trúc folder).
2. **Step 2: Domain logic & Types** (Template code mẫu rút từ code thật).
3. **Step 3: UI/API Integration** (Cách kết nối với bên ngoài).
4. **Step 4: Verification** (Chạy lệnh test/lint cụ thể).

**BẮT BUỘC:** Chèn các code templates (boilerplate) rút gọn từ code thật vào workflow để dev có thể khởi đầu nhanh.
```

---

## Prompt 3.2: Tạo `workflows/fix-bug-flow.md`

`````

Tạo quy trình chuẩn để fix bug dựa trên practices của dự án.

**Phân tích:**

1. Có testing framework nào? (Jest, Vitest, Cypress)
2. Có logging setup không?
3. Có error tracking (Sentry) không?
4. Git workflow đang dùng

**Output:**

````markdown
# Workflow: Fix Bug

## Bước 1: Reproduce & Document

- Tái hiện lỗi
- Ghi lại steps: ...
- Screenshot/Video nếu cần

## Bước 2: Viết Failing Test

```[language]
// Viết test case mô tả expected behavior
describe('[bug description]', () => {
  it('should [expected behavior]', () => {
    // ...
  });
});
`````

````

## Bước 3: Debug

- Đặt breakpoints tại [các file thường liên quan]
- Check console/network tab
- Dùng [logging tool của dự án]

## Bước 4: Fix & Verify

- Sửa code
- Chạy test: `[command]`
- Manual verify

## Bước 5: Commit

```bash
git add .
git commit -m "fix([scope]): [mô tả ngắn]

- Root cause: [nguyên nhân]
- Solution: [giải pháp]

Closes #[issue-number]"
```

```

```

---

# 📦 PHẦN 4: TEMPLATES

## Prompt 4.1: Tạo Template cho Component/Module chủ đạo

````

Xác định LOẠI COMPONENT/MODULE PHỔ BIẾN NHẤT trong dự án và tạo template.

**Bước 1: Thống kê**

- Đếm số lượng components theo loại
- Xác định pattern chung của loại phổ biến nhất

**Bước 2: Trích xuất template**

- Lấy 1 component "chuẩn" làm gốc
- Thay các giá trị cụ thể bằng placeholder
- Giữ nguyên structure, imports, patterns

**Output:**

````markdown
# Template: [Loại Component]

## Sử dụng Template này khi:

- [Điều kiện 1]
- [Điều kiện 2]

## Template Code

### File: `[ComponentName].tsx`

```tsx
import React from 'react';
// [import patterns từ dự án]

interface [ComponentName]Props {
  // Props thường dùng
}

export const [ComponentName]: React.FC<[ComponentName]Props> = ({
  // destructure
}) => {
  // hooks pattern của dự án

  return (
    // JSX structure pattern
  );
};
```
````

### File: `types.ts`

```ts
// Type definitions pattern
```

### File: `[componentName].test.tsx`

```tsx
// Test structure pattern
```

```

```

---

# 🧠 PHẦN 5: SKILLS (Kỹ năng Tư duy cho AI)

## Prompt 5.1: Tạo `skills/review-skill.md` - Tư duy Reviewer

```markdown
Phân tích lịch sử commits (`git log -n 50`) và các đoạn code có comment `TODO`, `FIXME`, `BUG` để tạo hướng dẫn review code tại `.agent/skills/review-skill.md`.

**TẬP TRUNG VÀO:**

1. **Lịch sử lỗi:** Dự án này hay gặp bug ở đâu? (vd: quên clean-up useEffect, sai logic phân trang).
2. **Naming Bad Patterns:** Những cách đặt tên nào từng bị refactor hoặc bị comment nhắc nhở?
3. **Logic Red Flags:** Liệt kê 5 "dấu hiệu nguy hiểm" trong dự án này (vd: gọi API trong loop, deep object nesting).

**MỤC TIÊU:** Skill này giúp AI khi được hỏi "Review code này" sẽ tập trung vào các vấn đề ĐẶC THÙ của dự án thay vì các lời khuyên Clean Code sáo rỗng.
```

---

## Prompt 5.2: Tạo `skills/debug-skill.md` - Tư duy Thám tử

```markdown
Hãy trở thành một Debugging Expert. Đọc `package.json` và cấu trúc dự án để tạo `.agent/skills/debug-skill.md`.

**CÁC BƯỚC PHÂN TÍCH:**

1. **Tooling:** Dự án dùng framework test gì? Có library logging nào không?
2. **Error Pattern:** Tìm cách project trả về error: Dùng Exceptions, Result Objects, hay chỉ `console.error`?
3. **Data Logging:** Chỉ ra các tệp hoặc dòng code đang thực hiện log dữ liệu "mẫu" để AI biết cách chèn log khi debug.

**MỤC TIÊU:** Khi AI gặp lỗi, nó sẽ kích hoạt Skill này để:

- Biết dùng lệnh test nào để reproduce.
- Biết chèn log vào đâu (theo convention dự án).
- Biết các lỗi "kinh điển" thường gặp ở dự án này.
```

---

## Prompt 5.3: Tạo `skills/performance-skill.md`

```
Tạo guide tối ưu performance dựa trên patterns và bottlenecks của dự án.

**Phân tích:**
1. Đang dùng optimization patterns nào? (React.memo, useMemo, useCallback)
2. Bundle có được split không? (lazy, Suspense)
3. Image optimization?
4. Caching strategies?

**Output:** Guide với metrics cụ thể và patterns từ code thật.
```

---

# 📚 PHẦN 6: DOCS (Knowledge Base)

## Prompt 6.1: Tạo `docs/architecture.md`

```
Phân tích và document kiến trúc hệ thống.

**Tạo:**
1. High-level architecture diagram (Mermaid)
2. Data flow chính
3. Key components và responsibilities
4. External dependencies và tích hợp
5. Environment configurations

**Output:** Tài liệu kiến trúc dễ hiểu cho dev mới join.
```

---

# 🧠 PHẦN 7: MEMORY (Bộ nhớ dài hạn)

## Prompt 7.1: Tạo `memory/project-context.md` - Phân tích toàn diện

**⏱️ Thời gian:** 10-15 phút | **📄 Target:** 100-150 dòng | **📊 Sections:** 8-10

```markdown
Bạn là một Senior Architect. Hãy phân tích TOÀN BỘ codebase hiện tại để tạo file hoàn chỉnh nhất: `.agent/memory/project-context.md`.

File này phải đóng vai trò là "Single Source of Truth" để bất kỳ AI nào sau này nhìn vào cũng hiểu dự án này là gì, hoạt động ra sao và đang ở đâu.

**YÊU CẦU PHÂN TÍCH CHUYÊN SÂU:**

1. **Project Identity (Tầm nhìn):**

   - Đọc README.md và Description để hiểu: Dự án này giải quyết bài toán gì? Cho ai?
   - Xác định Business Domain (Fintech, E-commerce, AI Tool, Health, v.v.).

2. **Tech Ecosystem (Hệ sinh thái):**

   - Đọc tệp quản lý dependency (`package.json`, `go.mod`, `requirements.txt`, v.v.).
   - Phân loại: Core Stack, Database, State Management, UI Library, Auth Provider, v.v.
   - Tìm các "Internal Tools" (tự viết) hoặc Utilities quan trọng.

3. **Architecture Architecture (Kiến trúc):**

   - Phân tích luồng dữ liệu: Client -> API -> Service -> Repo -> DB.
   - Xác định các Design Patterns đang dùng (Singleton, Factory, Observer, Dependency Injection, v.v.).
   - Mô tả cách giao tiếp giữa các thành phần (REST, GraphQL, WebSockets, gRPC).

4. **Logical Domains (Module nghiệp vụ):**

   - Liệt kê các module chính và trách nhiệm của từng cái (vd: Auth, Billing, Media Processing).

5. **Current State & Roadmap (Tiến độ):**

   - Quét toàn bộ codebase tìm `TODO`, `FIXME`, `HACK`.
   - Đối chiếu giữa file logic hiện có và mục tiêu trong README để biết cái nào đã xong, cái nào đang làm.

6. **Infrastructure & DevOps:**
   - Tìm file Docker, CI/CD, Script deploy để hiểu cách dự án vận hành thực tế.

**BẮT BUỘC:** Không viết lý thuyết suông. Mỗi mục phải có **file evidence** cụ thể đi kèm.

**OUTPUT TEMPLATE (Sử dụng format này):**

# 🧠 Project Context: [Tên Dự Án]

> Cập nhật cuối: [Ngày tháng năm] - Trạng thái: [WIP/Stable/Legacy]

## 1. 🎯 Tổng quan & Nghiệp vụ (Domain)

- **Mục đích:** [Mô tả ngắn gọn]
- **Business Logic:** [1-2 đoạn mô tả luồng quan trọng nhất - "Happy Path"]
- **User Persona:** [Ai là người dùng chính?]

## 2. 🛠️ Hệ sinh thái Công nghệ (Tech Stack)

| Layer     | Technologies        | Usage & Evidence       |
| --------- | ------------------- | ---------------------- |
| Runtime   | Node.js 20+         | `package.json`         |
| Framework | NestJS              | `src/main.ts`          |
| DB        | PostgreSQL + Prisma | `prisma/schema.prisma` |
| ...       | ...                 | ...                    |

## 3. 🏗️ Kiến trúc Hệ thống

- **Pattern:** [vd: Hexagonal Architecture / MVC / Monolith]
- **Data Flow:** [Mô tả ngắn gọn logic đi từ đâu đến đâu]
- **Key Files:** [Liệt kê 3-5 tệp "trái tim" của toàn hệ thống]

## 4. 📂 Quy hoạch Thư mục (Project Anatomy)

- `src/core/`: Chứa các logic dùng chung...
- `src/modules/`: Chứa các domain nghiệp vụ tách biệt...

## 5. 🚥 Trạng thái & Lộ trình (Development Status)

- [x] **Hoàn thành:** [Liệt kê các module đã ổn định]
- [ ] **Đang thực hiện:** [Liệt kê feature đang active]
- [ ] **Kế hoạch:** [Dựa vào README/TODO]

## 6. 🚧 Technical Debt & Known Issues

- **Issues:** [Liệt kê các bug khó hoặc FIXME quan trọng]
- **Debt:** [Những phần code đang là "tạm thời", cần refactor]

## 7. ⚙️ Cấu hình & Vận hành

- **Env:** [Các biến quan trọng từ .env.example]
- **Commands:** [Lệnh run/test/build quan trọng nhất]
```

---

# 🎭 PHẦN 8: MOCKS (Dữ liệu giả)

## Prompt 8.1: Tạo Mock Data - Dữ liệu thực chiến

```markdown
Phân tích các tệp định nghĩa Types/Interfaces quan trọng nhất (thực thể chính: User, Product, Transaction...) để tạo dữ liệu giả mẫu tại `.agent/mocks/sample-data.json`.

**YÊU CẦU:**

1. Với mỗi thực thể, tạo ít nhất 3 bộ dữ liệu:

   - **Happy Path:** Dữ liệu đầy đủ, chuẩn.
   - **Minimal Path:** Dữ liệu chỉ có các field bắt buộc.
   - **Edge Case:** Dữ liệu có chuỗi siêu dài, số âm, null/undefined ở các field optional.

2. Đảm bảo dữ liệu **TRÔNG NHƯ THẬT**: Tên người, email, ngày tháng phải hợp lý.
3. Dữ liệu phải parse được TypeScript interfaces của dự án.

**MỤC TIÊU:** AI dùng dữ liệu này để viết tests hoặc tạo UI demo nhanh mà không cần đợi API.
```

```json
// .agent/mocks/users.json
{
  "users": [
    {
      "id": "user-1",
      "name": "John Doe",
      "email": "john@example.com",
      "role": "admin"
    },
    {
      "id": "user-2",
      "name": "Jane Smith",
      "email": "jane@example.com",
      "role": "user"
    },
    {
      "id": "user-3",
      "name": "",
      "email": "edge-case@example.com",
      "role": "guest",
      "_note": "Edge case: empty name"
    }
  ]
}
```

---

# 🚀 PROMPT "MEGA ONE-SHOT" - Tạo toàn bộ .agent

```

Hãy phân tích TOÀN BỘ dự án [Frontend/Backend] này và tạo thư mục `.agent/` HOÀN CHỈNH.

**YÊU CẦU BẮT BUỘC:**

- Chỉ viết những gì RÚT RA TỪ CODE THẬT, không lý thuyết suông
- Nếu không chắc, ghi "[CẦN XÁC NHẬN]"
- Mỗi file ngắn gọn, actionable

**TẠO CÁC FOLDERS VÀ FILES:**

### 1. rules/ (Quy tắc - DỰA TRÊN CODE THẬT)

- global.md - Quy tắc chung (rút từ naming, structure, patterns)
- ui-components.md - Quy tắc UI (nếu có frontend)
- state-management.md - Quy tắc state
- api-integration.md - Quy tắc API

### 2. checklists/

- pr-review.md - Checklist review PR
- feature-deployment.md - Checklist deploy
- [domain].md - Checklist cho logic cốt lõi của dự án

### 3. workflows/

- create-new-feature.md - Quy trình tạo feature mới (với folder structure)
- fix-bug-flow.md - Quy trình fix bug

### 4. templates/

- [component-type].template.md - Template cho loại component phổ biến nhất

### 5. skills/

- review-skill.md - Cách review code
- debug-skill.md - Cách debug hiệu quả
- performance-skill.md - Cách tối ưu

### 6. docs/

- architecture.md - Kiến trúc hệ thống

### 7. memory/

- project-context.md - Context hiện tại + lessons learned

### 8. mocks/

- [entity].json - Mock data cho entities chính

**SAU KHI TẠO XONG, BÁO CÁO:**

1. Danh sách các files đã tạo
2. Giải thích ngắn tại sao mỗi quy tắc được đặt ra (dựa trên evidence từ code)
3. Những điều cần user xác nhận

```

---

## 💡 Pro Tips

1. **Chia nhỏ nếu dự án lớn:** Chạy từng prompt (rules → checklists → workflows...) thay vì mega one-shot.

2. **Verify từng output:** Sau mỗi file AI tạo, đọc qua và sửa những gì AI hiểu sai.

3. **Cập nhật liên tục:** `memory/project-context.md` nên được update sau mỗi sprint.

4. **Domain-specific rules:** Với mỗi module quan trọng (Auth, Payment, Camera...), có thể tạo thêm file rules riêng.

5. **Chạy lại khi refactor lớn:** Nếu có breaking changes lớn, nên regenerate lại các rules files.

---

# 🔍 PHẦN 9: VALIDATION - Kiểm tra kết quả AI tạo ra

## Prompt 9.1: Validate Rules - Thẩm định tính thực tế

```markdown
Hãy kiểm soát chất lượng file `.agent/rules/global.md`. Với mỗi quy tắc bạn đã viết, hãy thực hiện:

1. **Tìm bằng chứng:** Chỉ ra ít nhất 2 file khác nhau đang thực thi quy tắc này.
2. **Tìm "Kẻ phản bội":** Tìm bất kỳ tệp nào đang vi phạm quy tắc này (Ví dụ: rule "không dùng any" nhưng file X vẫn dùng).
3. **Chấm điểm:**
   - [ĐÃ XÁC MINH 100%]: Mọi nơi đều tuân thủ.
   - [XU THẾ CHÍNH]: Đa số tuân thủ, một vài chỗ cũ chưa refactor.
   - [AO TƯỞNG]: Quy tắc này không có thực tế trong code, hãy XÓA NÓ.

**Kết quả trả về:** Bảng tổng hợp chi tiết. Nếu quy tắc nào bị loại là "Ảo tưởng", hãy tự động cập nhật lại file rule.
```

---

## Prompt 9.2: Validate Completeness

```

Rà soát lại thư mục `.agent/` đã tạo và báo cáo:

1. **Files đã tạo:** (list)
2. **Files còn thiếu theo cấu trúc chuẩn:** (list)
3. **Files có nội dung quá sơ sài (< 20 dòng):** (list)
4. **Recommendations:** Những gì nên bổ sung thêm

Đặc biệt kiểm tra:

- [ ] rules/global.md có ít nhất 5 categories?
- [ ] checklists có ít nhất 10 items mỗi file?
- [ ] workflows có step-by-step commands cụ thể?
- [ ] skills có actionable patterns không chỉ lý thuyết?

```

---

# 🆘 PHẦN 10: TROUBLESHOOTING - Khi AI hiểu sai

## Prompt 10.1: Sửa Rules sai

```

File `.agent/rules/[tên file].md` có một số quy tắc KHÔNG ĐÚNG với thực tế dự án.

**Các quy tắc sai:**

1. [Quy tắc sai 1] - Thực tế là: [thực tế đúng]
2. [Quy tắc sai 2] - Thực tế là: [thực tế đúng]

**Yêu cầu:**

1. Sửa lại các quy tắc sai
2. Giữ nguyên các quy tắc đúng
3. Thêm evidence file cho mỗi quy tắc đã sửa

```

---

## Prompt 10.2: AI không hiểu cấu trúc dự án

```

Bạn đang hiểu sai cấu trúc dự án. Đây là clarification:

**Cấu trúc ĐÚNG:**

- [Giải thích folder nào làm gì]
- [Pattern thực sự đang dùng]

**Bạn đã HIỂU SAI:**

- [Điều AI nghĩ sai]

Hãy quét lại codebase với understanding mới này và cập nhật các file trong `.agent/`.

```

---

## Prompt 10.3: Output quá chung chung/lý thuyết

```

File `.agent/[tên file].md` bạn vừa tạo quá CHUNG CHUNG và LÝ THUYẾT.

**Vấn đề:**

- [Phần nào quá chung]

**Yêu cầu cụ thể:**

1. Với mỗi rule/guideline, phải có VÍ DỤ CODE THẬT từ dự án
2. Thay vì viết "should use TypeScript", viết "Dùng TypeScript như trong src/components/UserCard.tsx"
3. Thay vì viết "follow naming conventions", viết cụ thể pattern + ví dụ

Viết lại file với mức độ cụ thể cao hơn.

```

---

# 📊 PHẦN 11: PRIORITY ORDER - Thứ tự tạo files

## Thứ tự khuyến nghị (Quan trọng → Ít quan trọng)

```

TIER 1 - BẮT BUỘC (Tạo trước):
├── 1. memory/project-context.md # AI cần biết đang làm gì
├── 2. rules/global.md # Quy tắc nền tảng
└── 3. workflows/create-new-feature.md # Dùng hàng ngày

TIER 2 - QUAN TRỌNG (Tạo sau TIER 1):
├── 4. checklists/pr-review.md
├── 5. rules/[domain-specific].md # VD: ui-components.md
├── 6. workflows/fix-bug-flow.md
└── 7. skills/debug-skill.md

TIER 3 - NÂNG CAO (Khi đã ổn định):
├── 8. templates/[component].template.md
├── 9. skills/review-skill.md
├── 10. skills/performance-skill.md
├── 11. docs/architecture.md
└── 12. mocks/[entities].json

TIER 4 - OPTIONAL:
├── checklists/feature-deployment.md
└── Các rules bổ sung

```

## Prompt để tạo theo thứ tự

```

Hãy tạo thư mục `.agent/` theo thứ tự ưu tiên.

Bắt đầu với TIER 1 (3 files quan trọng nhất):

1. memory/project-context.md
2. rules/global.md
3. workflows/create-new-feature.md

Sau khi hoàn thành, hỏi tôi có muốn tiếp tục với TIER 2 không.

```

---

# 🎯 PHẦN 12: TRIGGER PHRASES - Khi nào AI dùng Skill nào

Thêm section này vào đầu mỗi file skill để AI biết khi nào kích hoạt:

## Prompt 12.1: Thêm Trigger Phrases - Kích hoạt tự động

```markdown
Duyệt qua tất cả các file trong `.agent/skills/`. Bạn hãy bổ sung một section "Trigger Phrases" vào đầu mỗi file.

**YÊU CẦU TƯ DUY:**

- Nghĩ về những câu hỏi "ngây ngô" nhất mà dev có thể hỏi (vd: "Sao code này đỏ?", "Check giùm cái này").
- Nghĩ về những tình huống "âm thầm" (vd: AI thấy user paste một đống log lỗi -> tự kích hoạt debug-skill).

**CẤU TRÚC TRIGGER:**

- **Ngôn ngữ:** Hỗ trợ cả Tiếng Anh và Tiếng Việt.
- **Context Trigger:** AI phải tự nhận diện tình huống (vd: "Khi thấy user nhắc đến hiệu năng hoặc lag").

**Ví dụ cho performance-skill.md:**

- User hỏi: "Sao nó lag thế?", "Optimize cái này", "Kiểm tra render".
- Context: Thấy user dùng map lồng nhau, hoặc render list lớn không có key.
```

---

# 📈 PHẦN 13: CONTINUOUS IMPROVEMENT

## Prompt 13.1: Cập nhật sau mỗi Sprint

```

Sprint [X] đã kết thúc. Hãy cập nhật các file trong `.agent/`:

**Những gì đã thay đổi:**

1. [Feature mới đã hoàn thành]
2. [Bugs đã fix - thêm vào lessons learned]
3. [Refactoring đã làm - cập nhật rules nếu cần]
4. [Dependencies mới - cập nhật docs]

**Files cần update:**

- [ ] memory/project-context.md - Cập nhật trạng thái
- [ ] rules/\*.md - Nếu có convention mới
- [ ] checklists/\*.md - Nếu phát hiện checklist item mới từ bugs

```

---

## Prompt 13.2: Review định kỳ (Monthly)

```

Hãy review toàn bộ thư mục `.agent/` và:

1. **Xóa những gì outdated:**

   - Rules không còn đúng
   - Workflows đã thay đổi
   - Memory items đã resolve

2. **Bổ sung những gì thiếu:**

   - Patterns mới xuất hiện trong code
   - Lessons learned từ bugs gần đây
   - Skills mới cần document

3. **Cải thiện quality:**
   - Thêm examples cho rules chung chung
   - Thêm commands cụ thể cho workflows
   - Consolidate duplicate content

**Output:** Summary của changes và list files đã update.

```

---

# ✅ TỔNG KẾT: Checklist hoàn chỉnh

Sau khi chạy xong các prompts, verify:

## Tier 1 (Must Have)

- [ ] `memory/project-context.md` - Có info về current work?
- [ ] `rules/global.md` - Có ít nhất 5 categories với examples?
- [ ] `workflows/create-new-feature.md` - Có folder structure + commands?

## Tier 2 (Should Have)

- [ ] `checklists/pr-review.md` - Có ít nhất 10 actionable items?
- [ ] `rules/[domain].md` - Cover main domain của dự án?
- [ ] `workflows/fix-bug-flow.md` - Có debugging steps cụ thể?
- [ ] `skills/debug-skill.md` - Có trigger phrases?

## Tier 3 (Nice to Have)

- [ ] `templates/*.md` - Có real code từ dự án?
- [ ] `skills/review-skill.md` - Có priority levels?
- [ ] `docs/architecture.md` - Có diagram (Mermaid)?
- [ ] `mocks/*.json` - Có edge cases?

## Quality Checks

- [ ] Mọi rule đều có evidence file từ codebase?
- [ ] Không có nội dung "lý thuyết suông"?
- [ ] Skills có trigger phrases?
- [ ] Workflows có commands thật?

```

```
