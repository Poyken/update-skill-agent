# 📘 Ví dụ thực tế: Tạo `.agent` cho Backend API

> Hướng dẫn từng bước với các **prompts có thể copy & paste ngay** để tạo `.agent` cho dự án Backend.

---

## 📋 Trước khi bắt đầu

### Yêu cầu:

- [ ] Có dự án Backend đang hoạt động (Node.js/Express, NestJS, hoặc tương tự)
- [ ] AI Agent có thể đọc code trong dự án (Cursor, Copilot, Claude Desktop)
- [ ] Dự án có ít nhất 5-10 files code để AI phân tích patterns

### Thời gian dự kiến: 30-45 phút

---

## 🚀 BƯỚC 1: Tạo folder structure (2 phút)

### Chạy lệnh này trong terminal:

```bash
# Tạo cấu trúc folder .agent
mkdir -p .agent/{memory,rules,workflows,checklists,skills,mocks}

# Verify
ls -la .agent/
```

**Expected output:**

```
drwxr-xr-x  checklists
drwxr-xr-x  memory
drwxr-xr-x  mocks
drwxr-xr-x  rules
drwxr-xr-x  skills
drwxr-xr-x  workflows
```

---

## 🚀 BƯỚC 2: Tạo `memory/project-context.md` (5 phút)

### Copy prompt này và paste vào AI:

````
Hãy tạo file .agent/memory/project-context.md cho dự án này.

**Yêu cầu phân tích:**
1. Đọc package.json để xác định tech stack chính xác
2. Quét folder structure để hiểu cấu trúc dự án
3. Tìm các TODO, FIXME trong code để biết việc chưa hoàn thành
4. Đọc README.md nếu có

**Output format BẮT BUỘC:**

```markdown
# Project Memory - [Tên dự án từ package.json]

> Cập nhật: [Ngày hôm nay]

## Mô tả
[1-2 câu về dự án]

## Tech Stack
| Layer | Công nghệ | Version |
|-------|-----------|---------|
| Runtime | [từ package.json] | [version] |
| Framework | [từ package.json] | [version] |
| Database | [từ code/config] | [version nếu có] |
| ORM | [từ package.json] | [version] |
...

## Cấu trúc thư mục
[Liệt kê các folders chính trong src/]

## Trạng thái hiện tại
- [x] [Những gì đã hoàn thành - dựa vào files có sẵn]
- [ ] [Những gì chưa hoàn thành - dựa vào TODO/FIXME]

## 🔄 Đang làm dở
[Nếu tìm thấy evidence của work in progress, ghi ở đây]
[Nếu không tìm thấy, ghi: "Chưa có thông tin - cần user cập nhật"]

## 🐛 Bugs/Issues đã biết
[Nếu tìm thấy FIXME hoặc known issues, ghi ở đây]

## ⚠️ Cấu hình quan trọng
[Các biến môi trường cần thiết từ .env.example hoặc config/]
````

**KHÔNG ĐƯỢC:** Đoán hoặc viết lý thuyết. Chỉ viết những gì TÌM THẤY trong code.
**NẾU KHÔNG TÌM THẤY:** Ghi "[CẦN USER CẬP NHẬT]"

```

### Sau khi AI tạo xong:

**Checklist verify:**
- [ ] Tech stack khớp với package.json?
- [ ] Folder structure đúng với thực tế?
- [ ] Không có nội dung đoán mò?

**Nếu có lỗi, dùng prompt này để sửa:**
```

File vừa tạo có vấn đề:

- [Mô tả vấn đề cụ thể]

Hãy đọc lại [file cụ thể] và sửa.

```

---

## 🚀 BƯỚC 3: Tạo `rules/global.md` (10 phút)

### Copy prompt này và paste vào AI:

```

Tạo file .agent/rules/global.md với các quy tắc code của dự án này.

**Phân tích BẮT BUỘC (mỗi mục phải có evidence file):**

1. **Naming Conventions:**

   - Quét 10 files trong src/ → tên files theo pattern gì?
   - Quét tên hàm, biến → camelCase, PascalCase, snake_case?
   - Tên folders → kebab-case, camelCase?

2. **File Structure:**

   - Mỗi module có những files gì? (controller, service, repository?)
   - Tests nằm ở đâu? (cạnh source hay folder riêng?)

3. **TypeScript:** (nếu dùng TS)

   - Có dùng 'any' không? (grep "any" trong src/)
   - Interface hay Type được ưu tiên?

4. **Error Handling:**

   - Có custom Error class không?
   - Pattern try-catch như thế nào?

5. **Database:**

   - ORM gì? Pattern gì? (Repository, Active Record?)
   - Có dùng transactions không?

6. **API Response:**
   - Format response như thế nào?
   - Các status codes nào được dùng?

**Output format BẮT BUỘC:**

````markdown
# Quy tắc Code - [Tên dự án]

> ⚠️ Rules dưới đây được RÚT RA TỪ CODE THỰC TẾ, không phải lý thuyết.

## 1. Naming Conventions

| Loại   | Pattern            | Evidence File      |
| ------ | ------------------ | ------------------ |
| [Loại] | [Pattern tìm thấy] | `[đường dẫn file]` |

**Ví dụ code thực tế:**

```[language]
// Từ [đường dẫn file]
[code snippet thật]
```
````

## 2. [Category tiếp theo]

[Tương tự với evidence + code example]
...

```

**❌ KHÔNG ĐƯỢC:**
- Viết "should", "best practice", "recommended"
- Tạo rules không có evidence file
- Copy từ documentation chung

**NẾU KHÔNG TÌM THẤY pattern:** Ghi "[KHÔNG TÌM THẤY - CẦN XÁC NHẬN]"
```

### Sau khi AI tạo xong:

**Checklist verify:**

- [ ] Mỗi rule có evidence file?
- [ ] Có code examples thực tế?
- [ ] Không có "should", "best practice"?

---

## 🚀 BƯỚC 4: Tạo `workflows/create-new-feature.md` (8 phút)

### Copy prompt này và paste vào AI:

````
Tạo file .agent/workflows/create-new-feature.md dựa trên pattern hiện có trong dự án.

**Phân tích cần làm:**
1. Xem một module hoàn chỉnh nhất (có nhiều files nhất) để làm mẫu
2. Liệt kê thứ tự các files cần tạo
3. Xác định scripts trong package.json (test, lint, build)
4. Tìm git conventions từ git log (nếu có)

**Output format:**

```markdown
# Workflow: Tạo Feature Mới

> Dựa trên pattern từ [tên module mẫu đã phân tích]

## Bước 1: Tạo branch
```bash
git checkout [main/develop - xem git convention]
git pull
git checkout -b feature/[feature-name]
````

## Bước 2: Tạo database (nếu cần table mới)

```bash
[Commands thực tế từ package.json hoặc ORM đang dùng]
```

## Bước 3: Tạo files

```
[Folder structure chính xác theo pattern dự án]
src/
├── [folder]/
│   ├── [file-pattern].ts
│   └── ...
```

## Bước 4: Template code

### 4.1 [File type 1]

```[language]
// Template dựa trên [evidence file]
[code template thực tế]
```

### 4.2 [File type 2]

[Tương tự]

## Bước 5: Test

```bash
[Test commands từ package.json scripts]
```

## Bước 6: Commit

```bash
git add .
git commit -m "[format từ git log nếu có, hoặc conventional commits]"
git push origin feature/[feature-name]
```

```

**QUAN TRỌNG:** Chỉ dùng commands và patterns TỪ DỰ ÁN THỰC TẾ này.
```

---

## 🚀 BƯỚC 5: Validate toàn bộ (5 phút)

### Copy prompt này để AI tự kiểm tra:

```
Hãy VALIDATE 3 files vừa tạo trong .agent/:

1. Đọc .agent/memory/project-context.md
2. Đọc .agent/rules/global.md
3. Đọc .agent/workflows/create-new-feature.md

Với MỖI file, kiểm tra:
- Có thông tin cụ thể của dự án này không? (không generic)
- Có evidence files/paths không?
- Có nội dung đoán mò không?

Output format:
| File | Specific? | Has Evidence? | Issues |
|------|-----------|---------------|--------|
| [file] | ✅/❌ | ✅/❌ | [Vấn đề nếu có] |

Nếu có issues, hãy sửa luôn.
```

---

## 🚀 BƯỚC 6: Quick Test (2 phút)

### Chạy prompt này để test AI có đọc được .agent không:

```
Không đọc bất kỳ file code nào khác, CHỈ dựa vào folder .agent/
hãy trả lời:

1. Dự án này dùng framework gì, version bao nhiêu?
2. Database là gì?
3. Khi tạo feature mới, cần tạo những files gì và ở đâu?
4. Naming convention cho files là gì?
```

**Nếu AI trả lời đúng → Setup thành công! 🎉**
**Nếu AI trả lời sai → Review lại các files trong .agent/**

---

## 📁 Kết quả sau khi hoàn thành

```
.agent/
├── memory/
│   └── project-context.md    ✅ (Tier 1 - bắt buộc)
├── rules/
│   └── global.md             ✅ (Tier 1 - bắt buộc)
├── workflows/
│   └── create-new-feature.md ✅ (Tier 1 - bắt buộc)
├── checklists/               (Tier 2 - làm sau)
├── skills/                   (Tier 2 - làm sau)
└── mocks/                    (Tier 3 - tùy chọn)
```

---

## 🔧 Tier 2: Bổ sung thêm (tùy chọn, 20 phút)

### Tạo `checklists/pr-review.md`:

````
Tạo file .agent/checklists/pr-review.md dựa trên rules đã tạo.

Yêu cầu:
- Mỗi item dựa trên 1 rule trong rules/global.md
- Có priority (Critical/Major/Minor)
- Có ít nhất 10 items

Output format:
```markdown
# PR Review Checklist

## Critical (Block merge)
- [ ] [Item dựa trên rule X]
- [ ] ...

## Major (Yêu cầu fix)
- [ ] ...

## Minor (Nice to have)
- [ ] ...
````

```

### Tạo `skills/debug-skill.md`:

```

Tạo file .agent/skills/debug-skill.md cho dự án này.

Phân tích:

- Xem devDependencies để biết debug tools nào có sẵn
- Tìm logging patterns trong code
- Xác định test framework

Output:

```markdown
# Debug Skill

## Khi nào áp dụng (Trigger Phrases)

- "lỗi", "bug", "error", "không hoạt động", "crash"
- "debug", "tìm nguyên nhân", "tại sao"

## Debug Tools có sẵn

| Tool              | Command   | Khi nào dùng |
| ----------------- | --------- | ------------ |
| [từ package.json] | [command] | [mô tả]      |

## Debug Flow

1. [Bước 1]
2. [Bước 2]
   ...

## Common Bugs trong dự án này

[Dựa trên FIXME, TODO, hoặc error patterns tìm thấy]
```

```

---

## 💡 Tips khi chạy prompts

| Vấn đề | Giải pháp |
|--------|-----------|
| AI output quá ngắn | Thêm: "Mở rộng với ít nhất 50 dòng" |
| AI viết lý thuyết | Thêm: "CHỈ viết những gì TÌM THẤY trong code" |
| AI không tìm thấy files | Hướng dẫn: "Xem folder [đường dẫn cụ thể]" |
| Output sai format | Copy lại phần format và yêu cầu làm theo chính xác |

---

## 🔄 Cập nhật định kỳ

### Sau mỗi Sprint (2 tuần):

```

Đọc các files trong .agent/ và:

1. Cập nhật trạng thái features trong memory/project-context.md
2. Thêm bugs mới đã fix vào "Lessons Learned"
3. Bổ sung rules mới nếu có pattern mới

```

### Sau refactoring lớn:

```

Folder structure đã thay đổi. Hãy:

1. Quét lại src/ và cập nhật cấu trúc trong memory/project-context.md
2. Kiểm tra rules/global.md còn đúng không, sửa nếu cần
3. Cập nhật workflows/create-new-feature.md với structure mới

```

---

## � Tài liệu liên quan

| Tài liệu | Link |
|----------|------|
| Hướng dẫn vận hành đầy đủ | [operation-guide.md](./operation-guide.md) |
| Bộ prompts chi tiết | [prompts-to-generate-agent.md](./prompts-to-generate-agent.md) |
| Validation checklist | [validation-checklist.md](./validation-checklist.md) |
| Pre-built template NestJS | [nestjs-prisma.md](./prebuilt-templates/nestjs-prisma.md) |

---

**⏱️ Tổng thời gian: ~30 phút cho Tier 1 | ~50 phút cho Tier 1+2**

**← Quay lại:** [Hướng dẫn vận hành](./operation-guide.md)
```
