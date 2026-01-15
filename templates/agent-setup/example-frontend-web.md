# 📗 Ví dụ thực tế: Tạo `.agent` cho Frontend Web

> Hướng dẫn từng bước với các **prompts có thể copy & paste ngay** để tạo `.agent` cho dự án Frontend.

---

## 📋 Trước khi bắt đầu

### Yêu cầu:

- [ ] Có dự án Frontend đang hoạt động (React, Next.js, Vue, hoặc tương tự)
- [ ] AI Agent có thể đọc code trong dự án (Cursor, Copilot, Claude Desktop)
- [ ] Dự án có ít nhất 5-10 components để AI phân tích patterns

### Thời gian dự kiến: 30-45 phút

---

## 🚀 BƯỚC 1: Tạo folder structure (2 phút)

### Chạy lệnh này trong terminal:

```bash
# Tạo cấu trúc folder .agent
mkdir -p .agent/{memory,rules,workflows,checklists,skills,templates}

# Verify
ls -la .agent/
```

**Expected output:**

```
drwxr-xr-x  checklists
drwxr-xr-x  memory
drwxr-xr-x  rules
drwxr-xr-x  skills
drwxr-xr-x  templates
drwxr-xr-x  workflows
```

---

## 🚀 BƯỚC 2: Tạo `memory/project-context.md` (5 phút)

### Copy prompt này và paste vào AI:

````
Hãy tạo file .agent/memory/project-context.md cho dự án Frontend này.

**Yêu cầu phân tích:**
1. Đọc package.json để xác định:
   - Framework (React, Next.js, Vue?)
   - Styling (TailwindCSS, CSS Modules, Styled Components?)
   - State management (Redux, Zustand, React Query?)
   - Form library (React Hook Form, Formik?)
2. Quét folder structure (src/, pages/, app/, components/)
3. Tìm các TODO, FIXME trong code
4. Đọc README.md và các config files (next.config.js, vite.config.ts)

**Output format BẮT BUỘC:**

```markdown
# Project Memory - [Tên dự án từ package.json]

> Cập nhật: [Ngày hôm nay]

## Mô tả
[1-2 câu về dự án]

## Tech Stack
| Layer | Công nghệ | Version | Ghi chú |
|-------|-----------|---------|---------|
| Framework | [Next.js/React/Vue] | [version] | [App Router/Pages Router?] |
| Styling | [TailwindCSS/CSS Modules] | [version] | |
| State (Client) | [Zustand/Redux/Context] | [version] | |
| State (Server) | [React Query/SWR/RTK Query] | [version] | |
| Forms | [React Hook Form/Formik] | [version] | |
| Testing | [Jest/Vitest/Playwright] | [version] | |

## Cấu trúc thư mục
````

src/
├── [liệt kê các folders chính]
...

```

## Trạng thái hiện tại
- [x] [Features đã hoàn thành - dựa vào code có sẵn]
- [ ] [Features chưa hoàn thành - dựa vào TODO/FIXME]

## 🔄 Đang làm dở
[Nếu tìm thấy evidence, ghi ở đây]
[Nếu không: "Chưa có thông tin - cần user cập nhật"]

## 🐛 Bugs/Issues đã biết
[FIXME hoặc known issues nếu tìm thấy]

## ⚠️ Cấu hình quan trọng
[Biến môi trường từ .env.example, CDN, API endpoints...]
```

**KHÔNG ĐƯỢC:** Đoán hoặc viết lý thuyết. Chỉ viết những gì TÌM THẤY trong code.
**NẾU KHÔNG TÌM THẤY:** Ghi "[CẦN USER CẬP NHẬT]"

```

### Sau khi AI tạo xong:

**Checklist verify:**
- [ ] Tech stack khớp với package.json?
- [ ] Folder structure đúng với thực tế?
- [ ] Biết được đang dùng App Router hay Pages Router? (nếu Next.js)
- [ ] Không có nội dung đoán mò?

---

## 🚀 BƯỚC 3: Tạo `rules/global.md` (10 phút)

### Copy prompt này và paste vào AI:

```

Tạo file .agent/rules/global.md với các quy tắc code của dự án Frontend này.

**Phân tích BẮT BUỘC (mỗi mục phải có evidence file):**

1. **Naming Conventions:**

   - Components: PascalCase hay kebab-case?
   - Hooks: useXxx pattern?
   - Files: .tsx hay .jsx? index.tsx hay ComponentName.tsx?

2. **Component Structure:**

   - Props: interface inline hay file riêng?
   - Default exports hay named exports?
   - Wrapper components có không?

3. **Styling:**

   - TailwindCSS? CSS Modules? Styled Components?
   - Có dùng cn() hay clsx() cho conditional classes?
   - Design tokens ở đâu?

4. **State Management:**

   - Client state dùng gì?
   - Server state dùng gì?
   - Pattern nào đang dùng?

5. **Import Order:**

   - Thứ tự imports như thế nào trong các file?
   - Có path aliases (@/, ~/) không?

6. **Forms:**
   - Library nào?
   - Validation dùng gì (Zod, Yup)?

**Output format BẮT BUỘC:**

````markdown
# Quy tắc Code - [Tên dự án]

> ⚠️ Rules được RÚT RA TỪ CODE THỰC TẾ, không phải lý thuyết.

## 1. Naming Conventions

| Loại       | Pattern   | Evidence File |
| ---------- | --------- | ------------- |
| Components | [pattern] | `[đường dẫn]` |
| Hooks      | [pattern] | `[đường dẫn]` |
| Types      | [pattern] | `[đường dẫn]` |

**Ví dụ code thực tế:**

```tsx
// Từ [đường dẫn file]
[code snippet thật]
```
````

## 2. Component Structure

[Với evidence files]

## 3. Styling

[Với evidence files]

...

```

**❌ KHÔNG ĐƯỢC viết:** "should", "best practice", "recommended"
**NẾU KHÔNG TÌM THẤY pattern:** Ghi "[KHÔNG TÌM THẤY - CẦN XÁC NHẬN]"
```

### Sau khi AI tạo xong:

**Checklist verify:**

- [ ] Mỗi rule có evidence file?
- [ ] Styling rules đúng với thực tế? (Tailwind vs CSS Modules)
- [ ] State management rules đúng?
- [ ] Không có "should", "best practice"?

---

## 🚀 BƯỚC 4: Tạo `rules/ui-components.md` (7 phút)

### Copy prompt này (đặc biệt quan trọng cho Frontend):

````
Tạo file .agent/rules/ui-components.md với quy tắc UI riêng.

**Phân tích 5 components lớn nhất:**
1. Props pattern như thế nào?
2. Loading/Error states handle ra sao?
3. Accessibility (aria-* labels)?
4. Responsive patterns?
5. Animation/Transitions?

**Output format:**

```markdown
# Quy tắc UI Components

## 1. Props Pattern
```tsx
// Evidence: [đường dẫn component]
interface ComponentProps {
  [pattern được dùng]
}
````

## 2. Loading States

```tsx
// Evidence: [đường dẫn]
if (isLoading) {
  return <Skeleton />; // hoặc pattern đang dùng
}
```

## 3. Error Handling

[Pattern error boundary hoặc error states]

## 4. Conditional Classes

```tsx
// Evidence: [đường dẫn]
className={cn(
  'base-classes',
  condition && 'conditional-classes'
)}
```

## 5. Form Components

[Pattern cho Input, Select, Checkbox...]

```

```

---

## 🚀 BƯỚC 5: Tạo `workflows/create-new-feature.md` (8 phút)

### Copy prompt này:

````
Tạo file .agent/workflows/create-new-feature.md dựa trên pattern hiện có.

**Phân tích:**
1. Tìm một feature/page hoàn chỉnh nhất để làm mẫu
2. Liệt kê các files cần tạo cho 1 feature mới
3. Xác định scripts từ package.json

**Output format:**

```markdown
# Workflow: Tạo Feature Mới

> Dựa trên pattern từ [tên feature/page mẫu]

## Bước 1: Tạo branch
```bash
git checkout main
git pull
git checkout -b feature/[feature-name]
````

## Bước 2: Tạo folder structure

### Nếu là Page mới:

```
src/
├── app/[feature-name]/        # (Next.js App Router)
│   └── page.tsx
# HOẶC
├── pages/[feature-name].tsx   # (Pages Router)
```

### Nếu là Component mới:

```
src/components/[FeatureName]/
├── index.tsx           # Main component
├── types.ts            # (nếu props phức tạp)
└── hooks.ts            # (nếu có custom hooks)
```

## Bước 3: Template Component

```tsx
// Template dựa trên [evidence file]
'use client'; // (nếu Next.js App Router)

interface [FeatureName]Props {
  // props
}

export function [FeatureName]({}: [FeatureName]Props) {
  // State hooks
  // Data fetching hooks (React Query nếu có)

  if (isLoading) return <Skeleton />;
  if (error) return <ErrorComponent />;

  return (
    <div>
      {/* content */}
    </div>
  );
}
```

## Bước 4: Tạo Hook (nếu cần data fetching)

```tsx
// src/hooks/use[FeatureName].ts
import { useQuery } from '@tanstack/react-query';

export function use[FeatureName]() {
  return useQuery({
    queryKey: ['[feature-name]'],
    queryFn: [service].getAll,
  });
}
```

## Bước 5: Test

```bash
[scripts từ package.json: npm run test, npm run lint]
```

## Bước 6: Commit

```bash
git add .
git commit -m "feat([feature]): add [feature]"
git push origin feature/[feature-name]
```

```

```

---

## 🚀 BƯỚC 6: Validate toàn bộ (5 phút)

### Copy prompt này để AI tự kiểm tra:

```
Hãy VALIDATE các files trong .agent/:

1. Đọc .agent/memory/project-context.md
2. Đọc .agent/rules/global.md
3. Đọc .agent/rules/ui-components.md (nếu có)
4. Đọc .agent/workflows/create-new-feature.md

Với MỖI file:
- Có thông tin cụ thể của dự án này không? (không generic)
- Có evidence files không?
- Có nội dung đoán mò không?

Output format:
| File | Specific? | Has Evidence? | Issues |
|------|-----------|---------------|--------|
| [file] | ✅/❌ | ✅/❌ | [vấn đề] |

Nếu có issues, sửa luôn.
```

---

## 🚀 BƯỚC 7: Quick Test (2 phút)

### Chạy prompt này để test:

```
Không đọc file code nào khác, CHỈ dựa vào folder .agent/
hãy trả lời:

1. Dự án này dùng framework gì? Styling gì?
2. State management client và server dùng gì?
3. Component mới nên đặt ở đâu? Theo pattern gì?
4. Props được định nghĩa bằng interface hay type? Ở đâu?
5. Khi tạo component mới có loading state, pattern nào được dùng?
```

**Nếu AI trả lời đúng → Setup thành công! 🎉**

---

## 📁 Kết quả sau khi hoàn thành

```
.agent/
├── memory/
│   └── project-context.md    ✅ (Tier 1)
├── rules/
│   ├── global.md             ✅ (Tier 1)
│   └── ui-components.md      ✅ (Tier 1 cho Frontend)
├── workflows/
│   └── create-new-feature.md ✅ (Tier 1)
├── checklists/               (Tier 2)
├── skills/                   (Tier 2)
└── templates/                (Tier 3)
```

---

## 🔧 Tier 2: Bổ sung thêm (tùy chọn, 20 phút)

### Tạo `skills/performance-skill.md` (Quan trọng cho Frontend):

````
Tạo file .agent/skills/performance-skill.md cho dự án này.

Phân tích:
- Components nào có memo/useMemo/useCallback?
- Có lazy loading không?
- Image optimization dùng gì?
- Bundle analyzer có không?

Output:
```markdown
# Performance Skill

## Khi nào áp dụng (Trigger Phrases)
- "chậm", "lag", "performance", "tối ưu"
- "re-render", "bundle size", "load time"

## Tools có sẵn
| Tool | Package | Command |
|------|---------|---------|
| [từ package.json] | | |

## Performance Checklist
- [ ] Components có re-render không cần thiết?
- [ ] Images đã optimize chưa?
- [ ] Bundle size hợp lý?
- [ ] Lazy loading cho routes?

## Common Performance Issues
[Dựa trên patterns tìm thấy trong code]
````

```

### Tạo `checklists/pr-review.md`:

```

Tạo file .agent/checklists/pr-review.md dựa trên rules đã tạo.

Yêu cầu riêng cho Frontend:

- TypeScript strict
- Accessibility
- Responsive
- Performance
- Styling consistency

Output:

```markdown
# PR Review Checklist - Frontend

## Critical

- [ ] TypeScript không có errors
- [ ] Components có loading/error states
- [ ] Responsive trên mobile

## Major

- [ ] Đúng naming conventions
- [ ] Props có TypeScript types
- [ ] Images dùng next/image (nếu Next.js)

## Minor

- [ ] Có alt text cho images
- [ ] Focus states cho interactive elements
```

```

### Tạo `templates/component.template.md`:

```

Tạo file .agent/templates/component.template.md dựa trên components hiện có.

Yêu cầu:

- Template cho component thông thường
- Template cho component có data fetching
- Template cho form component

Output là 3 templates có thể copy-paste.

```

---

## 💡 Tips khi chạy prompts cho Frontend

| Vấn đề | Giải pháp |
|--------|-----------|
| AI không biết dùng App Router hay Pages Router | Chỉ rõ: "Dự án dùng Next.js App Router" |
| AI viết rules cho CSS nhưng dùng Tailwind | Chỉ rõ: "Chỉ phân tích TailwindCSS patterns" |
| AI không tìm thấy state management | Hướng dẫn: "Xem folder src/store/ hoặc src/hooks/" |
| Output thiếu responsive rules | Thêm yêu cầu: "Bao gồm responsive patterns" |

---

## 🔄 Cập nhật định kỳ

### Sau mỗi Sprint:

```

Cập nhật .agent/:

1. Thêm components mới vào rules nếu có pattern mới
2. Cập nhật trạng thái features
3. Thêm bugs đã fix vào Lessons Learned

```

### Sau khi thêm thư viện mới:

```

Đã thêm [tên thư viện] vào dự án.
Hãy:

1. Cập nhật Tech Stack trong memory/project-context.md
2. Thêm rules mới vào rules/global.md nếu cần
3. Cập nhật workflows nếu flow thay đổi

```

---

## 📚 Tài liệu liên quan

| Tài liệu | Link |
|----------|------|
| Hướng dẫn vận hành đầy đủ | [operation-guide.md](./operation-guide.md) |
| Bộ prompts chi tiết | [prompts-to-generate-agent.md](./prompts-to-generate-agent.md) |
| Validation checklist | [validation-checklist.md](./validation-checklist.md) |
| Pre-built template Next.js | [nextjs-tailwind.md](./prebuilt-templates/nextjs-tailwind.md) |

---

**⏱️ Tổng thời gian: ~35 phút cho Tier 1 | ~55 phút cho Tier 1+2**

**← Quay lại:** [Hướng dẫn vận hành](./operation-guide.md)
```
