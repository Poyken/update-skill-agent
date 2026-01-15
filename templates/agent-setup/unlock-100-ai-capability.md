# 🚀 Hướng dẫn Sử dụng 100% Khả năng AI trong Phát triển Phần mềm

> Tài liệu này tổng hợp và giải thích cách tận dụng tối đa sức mạnh của AI thông qua việc thiết lập thư mục `.agent` một cách hoàn chỉnh.

---

## 📚 Mục lục

1. [Tổng quan: AI cần gì để hoạt động tối đa?](#-tổng-quan-ai-cần-gì-để-hoạt-động-tối-đa)
2. [8 Khả năng AI và cách Unlock](#-8-khả-năng-ai-và-cách-unlock)
3. [Lộ trình Setup từng bước](#-lộ-trình-setup-từng-bước)
4. [Cấu hình cho từng AI Tool](#-cấu-hình-cho-từng-ai-tool)
5. [Đo lường và Cải thiện liên tục](#-đo-lường-và-cải-thiện-liên-tục)
6. [Checklist hoàn chỉnh](#-checklist-hoàn-chỉnh)

---

## 🧠 Tổng quan: AI cần gì để hoạt động tối đa?

AI coding assistant (Cursor, GitHub Copilot, Claude, ChatGPT) có thể đạt hiệu suất từ **20%** đến **100%** tùy thuộc vào lượng context bạn cung cấp.

### So sánh AI có và không có `.agent`:

| Tiêu chí               | ❌ Không có `.agent`            | ✅ Có `.agent` đầy đủ                     |
| ---------------------- | ------------------------------- | ----------------------------------------- |
| **Hiểu dự án**         | Phải giải thích lại mỗi session | Tự động hiểu context                      |
| **Code quality**       | Code chung chung, cần sửa nhiều | Code đúng convention ngay từ đầu          |
| **Tốc độ**             | Nhiều lần hỏi - đáp             | Prompt 1 lần, nhận kết quả đúng           |
| **Nhất quán**          | Code style không đồng nhất      | Tuân thủ rules xuyên suốt                 |
| **Debug/Review**       | Không biết patterns của dự án   | Phát hiện lỗi theo đúng standards của bạn |
| **Onboarding dev mới** | Phải hỏi team lead              | Đọc `.agent` là hiểu ngay                 |

### 🎯 Mục tiêu: First-Prompt Success Rate ≥ 80%

Khi `.agent` được setup đúng, AI sẽ trả lời đúng/đủ **ngay từ prompt đầu tiên** ít nhất 80% số lần.

---

## 💎 8 Khả năng AI và cách Unlock

### Năng lực 1: Hiểu Context Dự án

| File cần có                        | Mô tả                               | Tài liệu tham khảo                                                                 |
| ---------------------------------- | ----------------------------------- | ---------------------------------------------------------------------------------- |
| `.agent/memory/project-context.md` | Mô tả dự án, tech stack, trạng thái | [Prompt 7.1](./prompts-to-generate-agent.md#prompt-71-tạo-memoryproject-contextmd) |

**Ví dụ nội dung:**

```markdown
# E-Commerce Dashboard

## Tech Stack

- Frontend: Next.js 14, TypeScript, TailwindCSS
- State: Zustand + React Query
- Backend: NestJS, Prisma, PostgreSQL

## Trạng thái hiện tại

- [x] Authentication (Hoàn thành)
- [/] Product Catalog (Đang làm - 70%)
- [ ] Payment Integration (Chưa bắt đầu)
```

---

### Năng lực 2: Viết Code Đúng Convention

| File cần có                        | Mô tả                         | Tài liệu tham khảo                                                                           |
| ---------------------------------- | ----------------------------- | -------------------------------------------------------------------------------------------- |
| `.agent/rules/global.md`           | Quy tắc code RÚT TỪ CODE THẬT | [Prompt 1.1](./prompts-to-generate-agent.md#prompt-11-tạo-rulesglobalmd---quy-tắc-chung)     |
| `.agent/rules/ui-components.md`    | Quy tắc riêng cho UI          | [Prompt 1.2](./prompts-to-generate-agent.md#prompt-12-tạo-rulesui-componentsmd---quy-tắc-ui) |
| `.agent/rules/state-management.md` | Quy tắc quản lý state         | [Prompt 1.3](./prompts-to-generate-agent.md#prompt-13-tạo-rulesstate-managementmd)           |

**⚠️ Quy tắc vàng:** Rules phải có:

- ✅ Evidence file: `src/components/UserCard.tsx`
- ✅ Code example thực tế
- ❌ KHÔNG ĐƯỢC có: "should", "best practice", "recommended"

---

### Năng lực 3: Tạo Feature Mới Đúng Cấu trúc

| File cần có                              | Mô tả                    |
| ---------------------------------------- | ------------------------ |
| `.agent/workflows/create-new-feature.md` | Quy trình step-by-step   |
| `.agent/templates/component.template.md` | Mẫu code để AI copy theo |

**Khi có workflow, AI sẽ:**

1. Tạo đúng folder structure
2. Tạo đủ các files cần thiết
3. Sử dụng đúng naming convention
4. Đăng ký routes/exports đúng chỗ

---

### Năng lực 4: Review Code Chất lượng

| File cần có                      | Mô tả                  |
| -------------------------------- | ---------------------- |
| `.agent/checklists/pr-review.md` | Checklist review PR    |
| `.agent/skills/review-skill.md`  | Cách tư duy khi review |

**AI có thể:**

- Phát hiện code smells theo standards của bạn
- Đề xuất improvements dựa trên patterns đã có
- Kiểm tra security, performance issues

---

### Năng lực 5: Debug Hiệu quả

| File cần có                    | Mô tả                            |
| ------------------------------ | -------------------------------- |
| `.agent/skills/debug-skill.md` | Tools + Debug flow theo loại bug |

**Nội dung debug skill:**

- List các developer tools đang dùng
- Debug flow cho từng loại bug (UI, State, API, Performance)
- Logging patterns của dự án
- Breakpoint strategies

---

### Năng lực 6: Tối ưu Performance

| File cần có                          | Mô tả                     |
| ------------------------------------ | ------------------------- |
| `.agent/skills/performance-skill.md` | Patterns tối ưu của dự án |
| `.agent/docs/architecture.md`        | Kiến trúc hệ thống        |

---

### Năng lực 7: Nhớ Context giữa các Sessions

| File cần có                        | Mô tả                               |
| ---------------------------------- | ----------------------------------- |
| `.agent/memory/project-context.md` | Đang làm dở, bugs đã fix, decisions |

**Sections quan trọng:**

- 🔄 Đang làm dở (feature, branch, status)
- 🐛 Bugs đã fix (root cause, solution, lesson learned)
- 🏗️ Architecture Decisions (context, options, rationale)
- ⚠️ Quirks & Workarounds

---

### Năng lực 8: Test với Mock Data

| File cần có           | Mô tả                 |
| --------------------- | --------------------- |
| `.agent/mocks/*.json` | Mock data cho test/UI |

**Bao gồm:**

- Normal cases
- Edge cases
- Empty states

---

## 📍 Lộ trình Setup từng bước

### ⏱️ Chọn phương pháp phù hợp

| Thời gian   | Phương pháp                                                              |
| ----------- | ------------------------------------------------------------------------ |
| **15 phút** | [Quick Start](./operation-guide.md#-quick-start-cho-người-vội---15-phút) |
| **20 phút** | Dùng [Pre-built Template](./prebuilt-templates/) cho stack của bạn       |
| **45 phút** | Tier 1 (3 files cốt lõi)                                                 |
| **90 phút** | Tier 1 + 2 (6 files)                                                     |
| **2+ giờ**  | Full setup (tất cả files)                                                |

### 🎯 Lộ trình NGƯỜI MỚI

#### Ngày 1: TIER 1 (30 phút) - BẮT BUỘC

| File                              | Thời gian | Prompt                                                                                   |
| --------------------------------- | --------- | ---------------------------------------------------------------------------------------- |
| `memory/project-context.md`       | 5 phút    | [Prompt 7.1](./prompts-to-generate-agent.md#prompt-71-tạo-memoryproject-contextmd)       |
| `rules/global.md`                 | 10 phút   | [Prompt 1.1](./prompts-to-generate-agent.md#prompt-11-tạo-rulesglobalmd---quy-tắc-chung) |
| `workflows/create-new-feature.md` | 8 phút    | [Prompt 3.1](./prompts-to-generate-agent.md#prompt-31-tạo-workflowscreate-new-featuremd) |

> **⏸️ CHECKPOINT:** Đọc qua 3 files, kiểm tra mỗi rule có evidence file không, sửa ngay nếu sai.

#### Ngày 2: TIER 2 (30 phút) - KHUYẾN NGHỊ

| File                      | Thời gian | Prompt                                                                                       |
| ------------------------- | --------- | -------------------------------------------------------------------------------------------- |
| `checklists/pr-review.md` | 8 phút    | [Prompt 2.1](./prompts-to-generate-agent.md#prompt-21-tạo-checklistspr-reviewmd)             |
| `rules/ui-components.md`  | 8 phút    | [Prompt 1.2](./prompts-to-generate-agent.md#prompt-12-tạo-rulesui-componentsmd---quy-tắc-ui) |
| `skills/debug-skill.md`   | 6 phút    | [Prompt 5.2](./prompts-to-generate-agent.md#prompt-52-tạo-skillsdebug-skillmd)               |

### 🚀 Lộ trình NGƯỜI ĐÃ CÓ KINH NGHIỆM

Chạy **MEGA ONE-SHOT** trong 45 phút:

```
Hãy phân tích TOÀN BỘ dự án này và tạo thư mục .agent/ HOÀN CHỈNH với:
- memory/project-context.md
- rules/global.md, rules/ui-components.md
- workflows/create-new-feature.md, workflows/fix-bug-flow.md
- checklists/pr-review.md
- skills/debug-skill.md, skills/review-skill.md

Yêu cầu:
- Chỉ viết những gì RÚT RA TỪ CODE THẬT
- Mỗi rule PHẢI có evidence file
- Nếu không chắc, ghi "[CẦN XÁC NHẬN]"
```

---

## 🔧 Cấu hình cho từng AI Tool

### Cursor

```bash
# .cursor/rules/rules.md được đọc tự động
cat .agent/memory/project-context.md > .cursor/rules/rules.md
cat .agent/rules/global.md >> .cursor/rules/rules.md
```

**Tips:**

- Giữ `rules.md` dưới 5000 từ
- Đặt rules quan trọng nhất ở đầu file

### GitHub Copilot

```bash
# .github/copilot/instructions.md được đọc tự động
mkdir -p .github/copilot
head -50 .agent/rules/global.md > .github/copilot/instructions.md
```

**Tips:**

- Context window nhỏ (~8K tokens)
- Chỉ include rules CẦN THIẾT NHẤT

### Claude

Claude không đọc folder tự động nhưng có context window RẤT LỚN (200K tokens).

**Cách dùng:**

1. Tạo file `claude-context.md` gộp các files quan trọng
2. Paste vào đầu mỗi session
3. Hoặc dùng Claude Projects để lưu persistent context

### ChatGPT

**Option 1:** Tạo Custom GPT (GPT Plus)

- Upload các files từ `.agent/` vào Knowledge base

**Option 2:** Manual context

- Summarize rules và paste vào đầu conversation

> 📖 Chi tiết: [tool-specific-configs.md](./tool-specific-configs.md)

---

## 📊 Đo lường và Cải thiện liên tục

### KPIs chính

| Metric                        | Target | Cách đo                                |
| ----------------------------- | ------ | -------------------------------------- |
| **First-Prompt Success Rate** | ≥ 80%  | AI trả lời đúng từ lần đầu tiên        |
| **Avg Iterations**            | ≤ 2    | Số lần phải yêu cầu AI sửa lại         |
| **Code Consistency Score**    | ≥ 80%  | Code AI generate có follow rules không |

### 🧪 Quick Test (chạy ngay sau khi setup)

```
Không đọc bất kỳ file nào khác, chỉ dựa vào .agent folder, hãy trả lời:
1. Dự án này dùng framework gì?
2. State management dùng gì?
3. Khi tạo feature mới, cần tạo những files gì?
```

→ Nếu AI trả lời đúng = Setup thành công! ✅

### 🔄 Bảo trì định kỳ

| Thời điểm            | Việc cần làm                             |
| -------------------- | ---------------------------------------- |
| **Sau mỗi Sprint**   | Update progress, thêm bugs đã fix        |
| **Hàng tháng**       | Xóa rules outdated, bổ sung patterns mới |
| **Khi refactor lớn** | Regenerate toàn bộ `rules/`              |
| **Khi đổi thư viện** | Update `docs/architecture.md`            |

> 📖 Chi tiết: [success-metrics.md](./success-metrics.md)

---

## ✅ Checklist hoàn chỉnh

### TIER 1 (Bắt buộc - 45 phút)

- [ ] `memory/project-context.md` - Có tech stack, trạng thái features
- [ ] `rules/global.md` - Có ≥5 categories với evidence files
- [ ] `workflows/create-new-feature.md` - Có folder structure + commands

### TIER 2 (Khuyến nghị - thêm 30 phút)

- [ ] `checklists/pr-review.md` - Có ≥10 actionable items
- [ ] `rules/ui-components.md` hoặc `rules/[domain].md`
- [ ] `skills/debug-skill.md` - Có trigger phrases

### TIER 3-4 (Nâng cao - thêm 45 phút)

- [ ] `templates/component.template.md`
- [ ] `skills/review-skill.md`
- [ ] `skills/performance-skill.md`
- [ ] `docs/architecture.md`
- [ ] `mocks/*.json`

### Quality Checks

- [ ] Mọi rule đều có evidence file từ codebase
- [ ] Không có nội dung "lý thuyết suông" (should, best practice)
- [ ] Skills có trigger phrases
- [ ] Workflows có commands thật

> 📖 Validation chi tiết: [validation-checklist.md](./validation-checklist.md)

---

## 🎯 Tổng kết

Để sử dụng **100% khả năng AI**, bạn cần:

1. **Setup đúng cách:** Tạo `.agent/` folder với đầy đủ context
2. **Cung cấp rules thực tế:** Rút từ code thật, không lý thuyết suông
3. **Cấu hình cho tool:** Sync sang `.cursor/` hoặc `.github/copilot/`
4. **Đo lường liên tục:** Track FPSR, iterations, code consistency
5. **Bảo trì định kỳ:** Update sau mỗi sprint, khi có thay đổi lớn

### 📚 Tài liệu tham khảo

| Tài liệu                                                       | Mô tả                        |
| -------------------------------------------------------------- | ---------------------------- |
| [operation-guide.md](./operation-guide.md)                     | Hướng dẫn vận hành chi tiết  |
| [prompts-to-generate-agent.md](./prompts-to-generate-agent.md) | 40+ prompts sẵn dùng         |
| [validation-checklist.md](./validation-checklist.md)           | Kiểm tra .agent đúng chưa    |
| [success-metrics.md](./success-metrics.md)                     | KPIs và cách đo lường        |
| [tool-specific-configs.md](./tool-specific-configs.md)         | Cấu hình cho từng AI tool    |
| [prebuilt-templates/](./prebuilt-templates/)                   | Templates sẵn cho các stacks |

---

**🏠 Quay về trang chính:** [README.md](./README.md)
