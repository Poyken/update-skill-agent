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

## Prompt 1.1: Tạo `rules/global.md` - Quy tắc chung

**⏱️ Thời gian:** 10 phút | **📄 Target:** 60-80 dòng | **📊 Sections:** 5-7

````
Quét toàn bộ codebase và RÚT RA các quy tắc code đang được tuân thủ THỰC TẾ để tạo file `.agent/rules/global.md`.

**QUAN TRỌNG:** Chỉ ghi những quy tắc BẠN THẤY TRONG CODE, không viết lý thuyết.

**❌ KHÔNG ĐƯỢC:**
- Viết "should use...", "best practice is...", "it's recommended to..."
- Tạo rules mà không có evidence file
- Copy từ documentation chung

**Phân tích các yếu tố:**

1. **Naming Conventions (Từ file names và biến):**
   - Quét 10 file trong src/components/ → rút ra pattern đặt tên
   - Quét 5 file hooks → xác định prefix (use...)
   - Quét constants → UPPER_CASE hay camelCase?

2. **File Structure (Từ cấu trúc folder):**
   - Mỗi component có folder riêng hay file đơn?
   - Có file index.ts barrel exports không?
   - Test files nằm cạnh source hay folder riêng?

3. **TypeScript Patterns (Từ các file .ts/.tsx):**
   - Có dùng 'any' không? (grep tìm "any")
   - Interface hay Type được ưu tiên?
   - Có strict mode không?

4. **Import/Export Style:**
   - Phân tích 5 file → thứ tự import như thế nào?
   - Default export hay named export?
   - Có path aliases không? (@/, ~/)

5. **Error Handling:**
   - Tìm các try-catch blocks
   - Có custom Error class không?
   - Console.log có được dùng không?

6. **Git Conventions (từ git log nếu có):**
   - Format commit message
   - Branch naming pattern

**Output Format (BẮT BUỘC theo format này):**
```markdown
# Quy tắc Code Chung - [Tên Dự Án]

> ⚠️ Các quy tắc này được rút ra từ code hiện có, KHÔNG phải lý thuyết.

## 1. Naming Conventions

| Loại | Pattern | Evidence File |
|------|---------|---------------|
| Components | PascalCase | `src/components/UserCard.tsx` |
| Hooks | camelCase + use | `src/hooks/useAuth.ts` |

**Ví dụ code thực tế:**
```tsx
// Từ src/components/UserCard.tsx
export function UserCard({ user }: UserCardProps) { ... }
```

## 2. File Organization
[Tương tự với evidence + example]

...
```
````

---

## Prompt 1.2: Tạo `rules/ui-components.md` - Quy tắc UI

**⏱️ Thời gian:** 8 phút | **📄 Target:** 50-70 dòng | **📊 Sections:** 5-6

```

Phân tích folder `src/components/` để tạo file `.agent/rules/ui-components.md`.

**❌ KHÔNG ĐƯỢC:** Viết lý thuyết về React/Vue chung. Chỉ viết những gì THẤY trong code.

**Kiểm tra:**

1. **Component Structure:**

   - Quét 5 component lớn nhất
   - Props được định nghĩa thế nào? (interface inline, type riêng, separate file)
   - Có destructure props không?
   - Default props xử lý ra sao?

2. **Styling Approach:**

   - TailwindCSS, CSS Modules, Styled-components, hay inline?
   - Có design tokens/theme không?
   - Responsive handling (breakpoints)

3. **State trong Components:**

   - useState được dùng như thế nào?
   - Có pattern controlled/uncontrolled?
   - Form handling: React Hook Form, Formik, hay native?

4. **Events & Callbacks:**

   - Naming: onClick, handleClick, hay onXxxClick?
   - Có useCallback cho optimization không?

5. **Conditional Rendering:**

   - Dùng && hay ternary?
   - Có early returns không?

6. **Accessibility:**
   - Có aria-\* attributes không?
   - Có alt text cho images không?
   - Keyboard navigation?

**Output:** File rules tập trung vào conventions UI component đã thấy trong code.

```

---

## Prompt 1.3: Tạo `rules/state-management.md`

```

Phân tích cách quản lý state trong dự án để tạo `.agent/rules/state-management.md`.

**Xác định State Solution:**

- Tìm trong package.json: redux, zustand, jotai, recoil, mobx?
- Hay chỉ dùng React Context + useState?
- Server state: React Query, SWR, Apollo?

**Nếu có Redux/Zustand:**

- Cấu trúc store như thế nào?
- Naming conventions cho actions, selectors
- Có middleware nào?

**Nếu dùng React Query:**

- Custom hooks pattern?
- Caching strategy?
- Invalidation logic?

**Context Usage:**

- Có bao nhiêu Context?
- Pattern: Provider ở đâu?
- Có tách read/write context không?

**Local State Rules:**

- Khi nào dùng useState vs global state?
- derived state được tính như thế nào?

**Output:** Rules cụ thể dựa trên patterns đã tìm thấy.

```

---

# ✅ PHẦN 2: CHECKLISTS

## Prompt 2.1: Tạo `checklists/pr-review.md`

````

Dựa trên code patterns và quy chuẩn đã phân tích, tạo checklist review Pull Request tại `.agent/checklists/pr-review.md`.

**Tạo checklist dựa trên THỰC TẾ dự án:**

1. **Từ Naming Conventions đã tìm:**

   - [ ] Tên biến/hàm/file có đúng pattern không?

2. **Từ TypeScript Usage:**

   - [ ] Có dùng 'any' không? (Nếu codebase không dùng any)
   - [ ] Types có được export đúng chỗ không?

3. **Từ Testing Pattern:**

   - [ ] Có unit test cho logic mới không?
   - [ ] Test có đúng structure không?

4. **Từ Error Handling:**

   - [ ] API calls có try-catch không?
   - [ ] Error messages có user-friendly không?

5. **Từ Performance Patterns:**

   - [ ] Có memo/useMemo/useCallback cần thiết không?
   - [ ] Có unnecessary re-renders không?

6. **Từ Security (nếu có):**
   - [ ] Có hardcode secrets không?
   - [ ] Input có được sanitize không?

**Format output:**

```markdown
# PR Review Checklist - [Tên dự án]

## Trước khi Review

- [ ] Branch đã rebase từ develop/main mới nhất
- [ ] Không có conflict

## Code Quality

- [ ] ...
````

```

---

## Prompt 2.2: Tạo `checklists/feature-deployment.md`

```

Tạo checklist deploy feature mới dựa trên cấu hình CI/CD và thực tế dự án.

**Phân tích:**

1. Đọc file cấu hình CI/CD (github workflows, gitlab-ci, docker-compose...)
2. Xem các scripts trong package.json
3. Tìm các bước build, test, deploy

**Tạo checklist:**

- Pre-deployment checks
- Build verification
- Testing requirements
- Environment variables
- Database migrations (nếu có)
- Rollback plan

**Output:** Checklist cụ thể với các commands thật từ dự án.

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

## Prompt 3.1: Tạo `workflows/create-new-feature.md`

```

Phân tích cấu trúc dự án để tạo workflow tạo feature mới.

**Phân tích:**

1. Cấu trúc folder của 1 feature hiện có (vd: src/features/auth/)
2. Các files thường có trong 1 feature
3. Naming patterns
4. Có generators/scripts sẵn không? (plop, hygen)

**Output Format:**

```markdown
# Workflow: Tạo Feature Mới

## Bước 1: Tạo folder structure

Tạo folder `src/features/[feature-name]/` với cấu trúc:
```

[feature-name]/
├── index.ts # Exports
├── [FeatureName].tsx # Main component
├── hooks/
│ └── use[FeatureName].ts
├── components/
├── types.ts
└── [feature-name].test.ts

```

## Bước 2: Tạo types (copy template sau)
[template thực tế từ code]

## Bước 3: Tạo hook
[template]

## Bước 4: Tạo component
[template]

## Bước 5: Export và Register
- Thêm vào router (nếu là page)
- Export từ index.ts
```

```

---

## Prompt 3.2: Tạo `workflows/fix-bug-flow.md`

```

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
```
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
```markdown
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

## Prompt 5.1: Tạo `skills/review-skill.md`

````
Dựa trên code patterns và common issues trong dự án, tạo hướng dẫn review code.

**Phân tích:**
1. Tìm các code smells phổ biến trong dự án (search TODO, FIXME, HACK)
2. Xác định các patterns thường bị vi phạm
3. Tìm các bugs đã fix gần đây (git log)

**Output:**
```markdown
# Skill: Code Review

## Mindset khi Review
1. Đọc qua toàn bộ diff trước khi comment
2. Focus vào logic, không nitpick formatting
3. Đặt câu hỏi thay vì chỉ trích

## Checklist theo thứ tự ưu tiên

### Critical (Block PR)
- [ ] Security vulnerabilities
- [ ] Data loss risks
- [ ] Breaking changes không document

### Major
- [ ] Logic errors
- [ ] Missing error handling
- [ ] Performance issues rõ ràng

### Minor
- [ ] Naming không theo convention
- [ ] Missing tests
- [ ] Code duplication

## Red Flags trong dự án này
(Dựa trên lịch sử bugs)
- ⚠️ [Pattern thường gây bug 1]
- ⚠️ [Pattern thường gây bug 2]

## Templates Comment
- "Có thể giải thích tại sao chọn approach này?"
- "Đã consider case [X] chưa?"
````

```

---

## Prompt 5.2: Tạo `skills/debug-skill.md`

```

Tạo hướng dẫn debug hiệu quả dựa trên tooling và patterns của dự án.

**Phân tích:**

1. Developer tools đang dùng (Redux DevTools, React DevTools...)
2. Logging setup
3. Error tracking (Sentry, LogRocket)
4. Testing tools

**Output:**

````markdown
# Skill: Debug Hiệu quả

## Tools có sẵn trong dự án

- [List tools từ devDependencies]

## Debug Flow theo loại Bug

### 1. UI không render đúng

- Check React DevTools → Component props
- Check CSS → Computed styles
- Check conditional rendering logic

### 2. State không update

- [Tool] DevTools → State tree
- Trace action/dispatch
- Check selectors

### 3. API Error

- Network tab → Request/Response
- Check error handling trong [file pattern]
- Verify mock data

### 4. Performance

- React DevTools Profiler
- Chrome Performance tab
- Check [common bottlenecks trong dự án]

## Logging Patterns trong dự án

```[language]
// Cách log đúng chuẩn dự án
[example từ code]
```
````

## Breakpoint Strategies

- Đặt tại [các điểm thường check]

```

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

## Prompt 7.1: Tạo `memory/project-context.md`

````
Tạo file lưu trữ context dự án để AI nhớ giữa các sessions.

**Content:**

1. **Đang làm dở:**
   - Feature hiện tại đang develop
   - Branch đang active
   - Blockers nếu có

2. **Lỗi khó đã fix (để không tái phạm):**
   - Bug description
   - Root cause
   - Solution
   - Lesson learned

3. **Decisions đã đưa ra:**
   - Tại sao chọn thư viện X thay vì Y
   - Architecture decisions và lý do

4. **Cần nhớ:**
   - Quirks của dự án
   - Workarounds đang dùng

**Output Template:**
```markdown
# Project Memory - [Tên dự án]

> Cập nhật: [DATE]

## 🔄 Đang làm dở
- **Feature:** [tên]
- **Branch:** [branch name]
- **Status:** [mô tả tiến độ]
- **Next steps:** [việc cần làm tiếp]

## 🐛 Bugs đã fix (Lessons Learned)

### Bug #1: [Tên bug]
- **Triệu chứng:** [...]
- **Nguyên nhân gốc:** [...]
- **Cách fix:** [...]
- **Bài học:** [...]

## 🏗️ Architecture Decisions

### Decision 1: [Tên]
- **Context:** [Bối cảnh khi quyết định]
- **Options considered:** [Các lựa chọn]
- **Decision:** [Quyết định cuối]
- **Rationale:** [Lý do]

## ⚠️ Quirks & Workarounds
- [Điều cần nhớ 1]
- [Điều cần nhớ 2]
````

```

---

# 🎭 PHẦN 8: MOCKS (Dữ liệu giả)

## Prompt 8.1: Tạo Mock Data

```

Phân tích types/interfaces trong dự án và tạo mock data.

**Bước 1: Tìm các types chính**

- Quét src/types/ hoặc các file types.ts
- Xác định entities chính (User, Product, Order...)

**Bước 2: Tạo mock data**

- Với mỗi type, tạo ít nhất 3 mock objects
- Cover các cases: normal, edge, empty

**Output:**

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

## Prompt 9.1: Validate Rules đã tạo

```

Hãy VERIFY lại file `.agent/rules/global.md` vừa tạo.

Với MỖI quy tắc đã viết, hãy:

1. Chỉ ra FILE CỤ THỂ trong codebase là evidence cho quy tắc đó
2. Nếu không tìm thấy evidence → đánh dấu "[KHÔNG CÓ BẰNG CHỨNG]"
3. Nếu có evidence mâu thuẫn (code vi phạm quy tắc) → ghi chú "[CÓ VI PHẠM tại file X]"

**Output Format:**

| Quy tắc                      | Evidence File                                             | Status                                    |
| ---------------------------- | --------------------------------------------------------- | ----------------------------------------- |
| "Components dùng PascalCase" | src/components/UserProfile.tsx, src/components/Header.tsx | ✅ Confirmed                              |
| "Không dùng any"             | ---                                                       | ❌ Có vi phạm tại src/utils/helpers.ts:45 |

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

## Prompt 12.1: Thêm Trigger Phrases vào Skills

```

Cập nhật các file trong `.agent/skills/` để thêm section "Trigger Phrases".

**Format cho mỗi skill file:**

```markdown
# Skill: [Tên Skill]

## 🎯 Khi nào dùng Skill này?

Kích hoạt skill này khi user nói:

- "[trigger phrase 1]"
- "[trigger phrase 2]"

HOẶC khi context cho thấy:

- [điều kiện 1]
- [điều kiện 2]
```

**Ví dụ cho debug-skill.md:**

```markdown
## 🎯 Khi nào dùng Skill này?

Kích hoạt khi user nói:

- "tại sao lỗi này xảy ra"
- "debug giúp tôi"
- "không hiểu tại sao code không chạy"
- "console báo lỗi"
- "app crash"

HOẶC khi context cho thấy:

- User paste error message/stack trace
- User mô tả unexpected behavior
- User nói "không hoạt động"
```

**Ví dụ cho review-skill.md:**

```markdown
## 🎯 Khi nào dùng Skill này?

Kích hoạt khi user nói:

- "review code này"
- "có vấn đề gì không"
- "code này ok chưa"
- "check giúp"

HOẶC khi context cho thấy:

- User paste một đoạn code mới viết
- User hỏi ý kiến về implementation
```

Hãy thêm Trigger Phrases phù hợp cho tất cả skill files.

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
