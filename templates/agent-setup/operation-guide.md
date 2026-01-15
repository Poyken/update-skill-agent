# 📖 HƯỚNG DẪN VẬN HÀNH - Tạo thư mục `.agent`

## Tổng quan quy trình

```
┌─────────────────────────────────────────────────────────────────┐
│                    QUY TRÌNH TẠO .AGENT                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  BƯỚC 1          BƯỚC 2          BƯỚC 3          BƯỚC 4        │
│  ┌──────┐       ┌──────┐        ┌──────┐        ┌──────┐       │
│  │ MỞ  │──────▶│ CHẠY │───────▶│VERIFY│───────▶│ SỬA  │       │
│  │ DỰ ÁN│       │PROMPT│        │OUTPUT│        │ LỖI  │       │
│  └──────┘       └──────┘        └──────┘        └──────┘       │
│      │              │               │               │          │
│      ▼              ▼               ▼               ▼          │
│  Mở folder     Copy prompt     Kiểm tra         Dùng prompt    │
│  gốc dự án     từ tài liệu     AI tạo đúng?     Troubleshoot   │
│                                                                 │
│                         ┌──────────────────┐                   │
│                         │   BƯỚC 5         │                   │
│                         │   CẬP NHẬT       │                   │
│                         │   ĐỊNH KỲ        │                   │
│                         └──────────────────┘                   │
└─────────────────────────────────────────────────────────────────┘
```

### 📚 Tài liệu liên quan

| Tài liệu                                               | Mô tả                              |
| ------------------------------------------------------ | ---------------------------------- |
| 📝 [Bộ Prompts đầy đủ](./prompts-to-generate-agent.md) | 40+ prompts sẵn dùng               |
| ✅ [Validation Checklist](./validation-checklist.md)   | Kiểm tra .agent đã đúng chưa       |
| 📊 [Success Metrics](./success-metrics.md)             | Đo lường hiệu quả + Quick Test     |
| ⚙️ [Tool-Specific Configs](./tool-specific-configs.md) | Cấu hình cho Cursor/Copilot/Claude |
| 📦 [Pre-built Templates](./prebuilt-templates/)        | Templates sẵn cho Next.js, NestJS  |

### 📘 Ví dụ thực tế

| Loại         | Link                                                                                          |
| ------------ | --------------------------------------------------------------------------------------------- |
| Backend API  | [example-backend-api.md](./example-backend-api.md) - E-Commerce API với Node.js/Express       |
| Frontend Web | [example-frontend-web.md](./example-frontend-web.md) - E-Commerce Dashboard với Next.js/React |

---

## ⚠️ Giới hạn của AI cần biết (ĐỌC TRƯỚC)

| Giới hạn                                    | Hậu quả                                     | Cách khắc phục                                                   |
| ------------------------------------------- | ------------------------------------------- | ---------------------------------------------------------------- |
| **AI không nhớ context giữa các sessions**  | Chạy prompt mới = AI quên hết output cũ     | Paste output của prompt trước vào chat khi chạy prompt tiếp theo |
| **AI hay đoán khi không tìm thấy evidence** | Viết rules "lý thuyết" thay vì từ code thật | Yêu cầu AI ghi `[KHÔNG TÌM THẤY - CẦN XÁC NHẬN]`                 |
| **AI có thể bỏ qua bước khi prompt dài**    | Output thiếu sections                       | Kiểm tra output có đủ sections không                             |
| **AI không biết file size phù hợp**         | File quá dài hoặc quá ngắn                  | Chỉ định "50-80 dòng" trong prompt                               |

### 📝 Quy tắc vàng khi làm việc với AI:

1. **Sau mỗi prompt:** Đọc qua output, sửa ngay nếu sai
2. **Khi chạy prompt tiếp:** Paste summary của output trước vào chat
3. **Khi AI đoán:** Yêu cầu chỉ rõ evidence file
4. **Khi output quá chung:** Dùng prompt "sửa output chung chung" (Prompt 10.3)

---

## BƯỚC 0: Chọn phương pháp phù hợp (2 phút)

### 🤔 Bạn thuộc trường hợp nào?

| Trường hợp                      | Phương pháp                                                                                    | Thời gian  |
| ------------------------------- | ---------------------------------------------------------------------------------------------- | ---------- |
| **Dự án Next.js + TailwindCSS** | Dùng [Pre-built Template](./prebuilt-templates/nextjs-tailwind.md)                             | 15 phút    |
| **Dự án NestJS + Prisma**       | Dùng [Pre-built Template](./prebuilt-templates/nestjs-prisma.md)                               | 15 phút    |
| **Dự án khác, muốn nhanh**      | Dùng [Quick Start](#-quick-start-cho-người-vội---15-phút)                                      | 15 phút    |
| **Dự án khác, muốn đầy đủ**     | Chạy từng prompt theo Tier 1-4                                                                 | 60-90 phút |
| **Người có kinh nghiệm**        | Dùng [MEGA ONE-SHOT](./prompts-to-generate-agent.md#-prompt-mega-one-shot---tạo-toàn-bộ-agent) | 45 phút    |

### 📋 Nếu dùng Pre-built Template:

```bash
# 1. Copy template vào dự án
mkdir -p .agent/{memory,rules,workflows,checklists,skills}

# 2. Mở template và chạy prompt customize
# Xem chi tiết: prebuilt-templates/[stack-name].md

# 3. Chạy Validation để kiểm tra
# Xem: validation-checklist.md
```

→ Sau đó nhảy đến **BƯỚC 3: Verify Output**

### 📋 Nếu tạo manual từ đầu:

→ Tiếp tục đọc từ **BƯỚC 1** bên dưới

---

## BƯỚC 1: Chuẩn bị (5 phút)

### 1.1 Mở dự án trong AI Agent

```bash
# Cursor
cursor /path/to/your/project

# VS Code + Copilot
code /path/to/your/project
```

### 1.2 Kiểm tra AI có quyền đọc codebase

- Đảm bảo AI có thể truy cập các files
- Test: Hỏi "Liệt kê các files trong src/"

### 1.3 Xác định loại dự án

- [ ] Frontend (React/Vue/Next.js...)
- [ ] Backend (Node/Express/NestJS...)
- [ ] Full-stack
- [ ] Khác: \***\*\_\_\_\*\***

---

## BƯỚC 2: Chạy Prompts theo thứ tự (30-60 phút)

### 🎯 Lộ trình cho NGƯỜI MỚI:

#### Ngày 1 (30 phút) - TIER 1

| STT | File cần tạo                      | Prompt     | ⏱️ Time | Link                                                                                     |
| --- | --------------------------------- | ---------- | ------- | ---------------------------------------------------------------------------------------- |
| 1   | `memory/project-context.md`       | Prompt 7.1 | 5 phút  | [Xem prompt](./prompts-to-generate-agent.md#prompt-71-tạo-memoryproject-contextmd)       |
| 2   | `rules/global.md`                 | Prompt 1.1 | 10 phút | [Xem prompt](./prompts-to-generate-agent.md#prompt-11-tạo-rulesglobalmd---quy-tắc-chung) |
| 3   | `workflows/create-new-feature.md` | Prompt 3.1 | 8 phút  | [Xem prompt](./prompts-to-generate-agent.md#prompt-31-tạo-workflowscreate-new-featuremd) |

→ Sau đó chạy [Validation](./prompts-to-generate-agent.md#-phần-9-validation---kiểm-tra-kết-quả-ai-tạo-ra)

#### ⏸️ CHECKPOINT SAU TIER 1 (BẮT BUỘC)

```
□ Đọc qua 3 files đã tạo (5 phút)
□ Kiểm tra: Mỗi rule có evidence file không?
□ Sửa những gì AI viết sai hoặc đoán
□ Paste SUMMARY của output vào chat trước khi chạy Tier 2

Ví dụ summary để paste:
"Đã tạo xong 3 files: project-context.md (mô tả E-commerce app, Next.js),
rules/global.md (6 rules về naming, structure), workflow/create-feature.md.
Tiếp tục tạo Tier 2."
```

---

#### Ngày 2 (30 phút) - TIER 2

| STT | File cần tạo              | Prompt     | ⏱️ Time | Link                                                                                         |
| --- | ------------------------- | ---------- | ------- | -------------------------------------------------------------------------------------------- |
| 4   | `checklists/pr-review.md` | Prompt 2.1 | 8 phút  | [Xem prompt](./prompts-to-generate-agent.md#prompt-21-tạo-checklistspr-reviewmd)             |
| 5   | `rules/ui-components.md`  | Prompt 1.2 | 8 phút  | [Xem prompt](./prompts-to-generate-agent.md#prompt-12-tạo-rulesui-componentsmd---quy-tắc-ui) |
| 6   | `skills/debug-skill.md`   | Prompt 5.2 | 6 phút  | [Xem prompt](./prompts-to-generate-agent.md#prompt-52-tạo-skillsdebug-skillmd)               |

→ Chạy [Validation](./prompts-to-generate-agent.md#-phần-9-validation---kiểm-tra-kết-quả-ai-tạo-ra)

#### ⏸️ CHECKPOINT SAU TIER 2

```
□ Kiểm tra checklist có ít nhất 10 items không?
□ Skills có trigger phrases không?
□ Quyết định: Đủ dùng hay cần thêm Tier 3-4?
```

---

#### Tuần sau - TIER 3-4 (khi cần)

| File cần tạo             | Prompt     | ⏱️ Time | Link                                                                                            |
| ------------------------ | ---------- | ------- | ----------------------------------------------------------------------------------------------- |
| `templates/*.md`         | Prompt 4.1 | 10 phút | [Xem prompt](./prompts-to-generate-agent.md#prompt-41-tạo-template-cho-componentmodule-chủ-đạo) |
| `skills/review-skill.md` | Prompt 5.1 | 6 phút  | [Xem prompt](./prompts-to-generate-agent.md#prompt-51-tạo-skillsreview-skillmd)                 |
| `docs/architecture.md`   | Prompt 6.1 | 8 phút  | [Xem prompt](./prompts-to-generate-agent.md#prompt-61-tạo-docsarchitecturemd)                   |
| `mocks/*.json`           | Prompt 8.1 | 5 phút  | [Xem prompt](./prompts-to-generate-agent.md#prompt-81-tạo-mock-data)                            |

---

### ⚡ Lộ trình cho NGƯỜI ĐÃ CÓ KINH NGHIỆM:

**1 lần duy nhất (45 phút):**

| Bước | Hành động                   | Link                                                                                             |
| ---- | --------------------------- | ------------------------------------------------------------------------------------------------ |
| 1    | Chạy Prompt "MEGA ONE-SHOT" | [Xem prompt](./prompts-to-generate-agent.md#-prompt-mega-one-shot---tạo-toàn-bộ-agent)           |
| 2    | Chạy Validation             | [Xem prompt](./prompts-to-generate-agent.md#prompt-91-validate-rules-đã-tạo)                     |
| 3    | Sửa lỗi (nếu có)            | [Xem Troubleshooting](./prompts-to-generate-agent.md#-phần-10-troubleshooting---khi-ai-hiểu-sai) |

---

## BƯỚC 3: Verify Output (10-15 phút)

### 3.1 Chạy prompt Validation

👉 [Prompt 9.1: Validate Rules](./prompts-to-generate-agent.md#prompt-91-validate-rules-đã-tạo)
👉 [Prompt 9.2: Validate Completeness](./prompts-to-generate-agent.md#prompt-92-validate-completeness)

### 3.2 Checklist kiểm tra nhanh

**Tier 1 Files:**

- [ ] `memory/project-context.md` tồn tại?
- [ ] `rules/global.md` có ít nhất 5 mục?
- [ ] `workflows/create-new-feature.md` có commands cụ thể?

**Quality Check:**

- [ ] Mỗi rule có VÍ DỤ từ code thật?
- [ ] Không có nội dung "lý thuyết suông"?
- [ ] Tên files/folders trong output đúng với thực tế?

### 3.3 Nếu phát hiện lỗi

→ Chuyển sang **BƯỚC 4: Troubleshooting**

---

## BƯỚC 4: Xử lý lỗi (Nếu cần)

### Bảng tra cứu lỗi → prompt:

| Lỗi gặp phải                     | Mô tả chi tiết                                       | Giải pháp                                                                                |
| -------------------------------- | ---------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Output quá chung chung**       | AI viết "should use...", "best practice is..."       | [Prompt 10.3](./prompts-to-generate-agent.md#prompt-103-output-quá-chung-chunglý-thuyết) |
| **AI hiểu sai cấu trúc**         | AI nghĩ dùng Redux nhưng thực tế dùng Zustand        | [Prompt 10.2](./prompts-to-generate-agent.md#prompt-102-ai-không-hiểu-cấu-trúc-dự-án)    |
| **Rules không có evidence**      | AI viết rule nhưng không chỉ ra file nào             | [Prompt 9.1](./prompts-to-generate-agent.md#prompt-91-validate-rules-đã-tạo)             |
| **Thiếu files**                  | Chỉ tạo 2/3 files được yêu cầu                       | [Prompt 9.2](./prompts-to-generate-agent.md#prompt-92-validate-completeness)             |
| **Rules sai thực tế**            | AI ghi "dùng class-validator" nhưng thực tế dùng Zod | [Prompt 10.1](./prompts-to-generate-agent.md#prompt-101-sửa-rules-sai)                   |
| **File rỗng/quá ngắn**           | AI tạo file chỉ có 10 dòng                           | Yêu cầu: "Mở rộng file này với ít nhất 50 dòng, thêm examples"                           |
| **Duplicate content**            | Nội dung giống nhau trong 2 files                    | Yêu cầu: "Gộp nội dung trùng lặp, xóa file redundant"                                    |
| **AI tạo folder sai**            | Tạo `.agent` thay vì `.agent/rules/`                 | Yêu cầu: "Tạo đúng cấu trúc folder: .agent/[subfolder]/[file].md"                        |
| **Không chạy được prompts tiếp** | AI nói "không có context"                            | Paste summary của output trước vào chat                                                  |
| **Quá nhiều [CẦN XÁC NHẬN]**     | AI không tìm được patterns                           | Cung cấp thêm context: "Project dùng [tech X], xem file [path]"                          |

### Quy trình sửa lỗi:

```
1. Xác định lỗi thuộc loại nào (tra bảng trên)
2. Click link để mở prompt tương ứng
3. Copy prompt và điền thông tin cụ thể vào [placeholder]
4. Chạy prompt
5. Verify lại bằng Prompt 9.1 hoặc 9.2
```

### Template sửa lỗi nhanh:

```
Output trước đó có vấn đề:
- [Mô tả vấn đề]

Yêu cầu sửa:
- [Yêu cầu cụ thể]

Thông tin bổ sung:
- File reference: [đường dẫn]
- Thực tế đúng là: [thông tin]
```

---

## BƯỚC 5: Bảo trì định kỳ

### 5.1 Sau mỗi Sprint (2 tuần)

👉 [Prompt 13.1: Cập nhật sau Sprint](./prompts-to-generate-agent.md#prompt-131-cập-nhật-sau-mỗi-sprint)

**Việc cần làm:**

- Update `memory/project-context.md`
- Thêm bugs đã fix vào lessons learned
- Cập nhật progress cho features mới

### 5.2 Hàng tháng

👉 [Prompt 13.2: Review định kỳ](./prompts-to-generate-agent.md#prompt-132-review-định-kỳ-monthly)

**Việc cần làm:**

- Xóa rules đã outdated
- Bổ sung patterns mới phát hiện
- Consolidate duplicate content

### 5.3 Khi có thay đổi lớn

| Thay đổi               | Hành động                     |
| ---------------------- | ----------------------------- |
| Refactor lớn           | Regenerate toàn bộ `rules/`   |
| Đổi thư viện/framework | Update `docs/architecture.md` |
| Team member mới join   | Review và bổ sung tất cả      |
| Đổi conventions        | Regenerate `rules/global.md`  |

---

## 🚀 QUICK START (Cho người vội - 15 phút)

Nếu bạn chỉ có **15 phút**, làm theo các bước sau:

### Bước 1: Mở dự án

```bash
cursor /path/to/your/project
```

### Bước 2: Copy và chạy prompt này

```
Hãy tạo thư mục .agent/ với 3 files quan trọng nhất:

1. memory/project-context.md
   - Mô tả dự án, tech stack, trạng thái hiện tại

2. rules/global.md
   - Quy tắc code RÚT TỪ CODE THẬT trong dự án
   - Mỗi rule PHẢI có ví dụ file thực tế

3. workflows/create-new-feature.md
   - Quy trình tạo feature mới với folder structure cụ thể

Yêu cầu bắt buộc:
- Chỉ viết những gì RÚT RA TỪ CODE THẬT
- Mỗi rule phải có ví dụ file thực tế từ codebase
- Nếu không chắc, ghi "[CẦN XÁC NHẬN]"
```

### Bước 3: Kiểm tra output

- [ ] 3 files đã được tạo?
- [ ] Có examples từ code thật?

### Bước 4: Bổ sung sau

Khi có thời gian, quay lại và chạy thêm các prompts từ [file prompts đầy đủ](./prompts-to-generate-agent.md).

---

## 📍 Mục lục nhanh - Tìm prompt theo nhu cầu

| Tôi muốn...            | Prompt | Link trực tiếp                                                                                    |
| ---------------------- | ------ | ------------------------------------------------------------------------------------------------- |
| Tạo rules chung        | 1.1    | [→ Xem](./prompts-to-generate-agent.md#prompt-11-tạo-rulesglobalmd---quy-tắc-chung)               |
| Tạo rules UI           | 1.2    | [→ Xem](./prompts-to-generate-agent.md#prompt-12-tạo-rulesui-componentsmd---quy-tắc-ui)           |
| Tạo rules state        | 1.3    | [→ Xem](./prompts-to-generate-agent.md#prompt-13-tạo-rulesstate-managementmd)                     |
| Tạo checklist PR       | 2.1    | [→ Xem](./prompts-to-generate-agent.md#prompt-21-tạo-checklistspr-reviewmd)                       |
| Tạo checklist deploy   | 2.2    | [→ Xem](./prompts-to-generate-agent.md#prompt-22-tạo-checklistsfeature-deploymentmd)              |
| Tạo checklist domain   | 2.3    | [→ Xem](./prompts-to-generate-agent.md#prompt-23-tạo-checklist-cho-logic-cốt-lõi-domain-specific) |
| Tạo workflow feature   | 3.1    | [→ Xem](./prompts-to-generate-agent.md#prompt-31-tạo-workflowscreate-new-featuremd)               |
| Tạo workflow fix bug   | 3.2    | [→ Xem](./prompts-to-generate-agent.md#prompt-32-tạo-workflowsfix-bug-flowmd)                     |
| Tạo template           | 4.1    | [→ Xem](./prompts-to-generate-agent.md#prompt-41-tạo-template-cho-componentmodule-chủ-đạo)        |
| Tạo review skill       | 5.1    | [→ Xem](./prompts-to-generate-agent.md#prompt-51-tạo-skillsreview-skillmd)                        |
| Tạo debug skill        | 5.2    | [→ Xem](./prompts-to-generate-agent.md#prompt-52-tạo-skillsdebug-skillmd)                         |
| Tạo performance skill  | 5.3    | [→ Xem](./prompts-to-generate-agent.md#prompt-53-tạo-skillsperformance-skillmd)                   |
| Tạo docs architecture  | 6.1    | [→ Xem](./prompts-to-generate-agent.md#prompt-61-tạo-docsarchitecturemd)                          |
| Tạo memory context     | 7.1    | [→ Xem](./prompts-to-generate-agent.md#prompt-71-tạo-memoryproject-contextmd)                     |
| Tạo mock data          | 8.1    | [→ Xem](./prompts-to-generate-agent.md#prompt-81-tạo-mock-data)                                   |
| **Tạo TẤT CẢ**         | MEGA   | [→ Xem](./prompts-to-generate-agent.md#-prompt-mega-one-shot---tạo-toàn-bộ-agent)                 |
| Validate rules         | 9.1    | [→ Xem](./prompts-to-generate-agent.md#prompt-91-validate-rules-đã-tạo)                           |
| Validate hoàn chỉnh    | 9.2    | [→ Xem](./prompts-to-generate-agent.md#prompt-92-validate-completeness)                           |
| Sửa rules sai          | 10.1   | [→ Xem](./prompts-to-generate-agent.md#prompt-101-sửa-rules-sai)                                  |
| Sửa AI hiểu sai        | 10.2   | [→ Xem](./prompts-to-generate-agent.md#prompt-102-ai-không-hiểu-cấu-trúc-dự-án)                   |
| Sửa output chung chung | 10.3   | [→ Xem](./prompts-to-generate-agent.md#prompt-103-output-quá-chung-chunglý-thuyết)                |
| Thêm trigger phrases   | 12.1   | [→ Xem](./prompts-to-generate-agent.md#prompt-121-thêm-trigger-phrases-vào-skills)                |
| Cập nhật sau sprint    | 13.1   | [→ Xem](./prompts-to-generate-agent.md#prompt-131-cập-nhật-sau-mỗi-sprint)                        |
| Review định kỳ         | 13.2   | [→ Xem](./prompts-to-generate-agent.md#prompt-132-review-định-kỳ-monthly)                         |

---

## ✅ Checklist tổng kết

Sau khi hoàn thành, verify:

### Tier 1 (Bắt buộc)

- [ ] `memory/project-context.md` - Có info về current work?
- [ ] `rules/global.md` - Có ít nhất 5 categories với examples?
- [ ] `workflows/create-new-feature.md` - Có folder structure + commands?

### Tier 2 (Nên có)

- [ ] `checklists/pr-review.md` - Có ít nhất 10 actionable items?
- [ ] `rules/[domain].md` - Cover main domain của dự án?
- [ ] `skills/debug-skill.md` - Có trigger phrases?

### Quality Checks

- [ ] Mọi rule đều có evidence file từ codebase?
- [ ] Không có nội dung "lý thuyết suông"?
- [ ] Skills có trigger phrases?
- [ ] Workflows có commands thật?

👉 **Validation chi tiết:** Chạy [validation-checklist.md](./validation-checklist.md) để kiểm tra đầy đủ

---

## 🎉 Sau khi hoàn thành

### Bước tiếp theo:

| Việc cần làm              | Tài liệu                                                                  | Mục đích                         |
| ------------------------- | ------------------------------------------------------------------------- | -------------------------------- |
| **Test AI có đọc .agent** | [success-metrics.md](./success-metrics.md#-quick-test-prompts)            | Kiểm tra AI hiểu context         |
| **Cấu hình cho AI tool**  | [tool-specific-configs.md](./tool-specific-configs.md)                    | Tối ưu cho Cursor/Copilot/Claude |
| **Đo lường hiệu quả**     | [success-metrics.md](./success-metrics.md)                                | Track KPIs sau 1 tuần            |
| **Cập nhật định kỳ**      | [Phần 13](./prompts-to-generate-agent.md#-phần-13-continuous-improvement) | Sau mỗi sprint                   |

### Quick Test (chạy ngay sau khi setup):

```
Prompt test:
"Không đọc bất kỳ file nào khác, chỉ dựa vào .agent folder, hãy trả lời:
1. Dự án này dùng framework gì?
2. State management dùng gì?
3. Khi tạo feature mới, cần tạo những files gì?"

→ Nếu AI trả lời đúng = Setup thành công!
→ Nếu sai = Review lại files trong .agent/
```

### Sync với các AI tools khác (tuỳ chọn):

```bash
# Nếu dùng nhiều tools, chạy sync script
# Chi tiết: tool-specific-configs.md

# Quick sync to Cursor
cat .agent/memory/project-context.md > .cursor/rules/rules.md
cat .agent/rules/global.md >> .cursor/rules/rules.md
```

---

## 📊 Tổng kết thời gian

| Phương pháp            | BƯỚC 0 | BƯỚC 1 | BƯỚC 2 | BƯỚC 3 | BƯỚC 4 | Tổng         |
| ---------------------- | ------ | ------ | ------ | ------ | ------ | ------------ |
| **Pre-built Template** | 2'     | -      | 10'    | 5'     | 5'     | **~20 phút** |
| **Quick Start**        | 2'     | 3'     | 10'    | 5'     | 5'     | **~25 phút** |
| **Tier 1 only**        | 2'     | 5'     | 25'    | 10'    | 5'     | **~45 phút** |
| **Tier 1+2**           | 2'     | 5'     | 50'    | 15'    | 10'    | **~80 phút** |
| **Full (Tier 1-4)**    | 2'     | 5'     | 80'    | 20'    | 15'    | **~2 giờ**   |
| **MEGA ONE-SHOT**      | 2'     | 5'     | 30'    | 15'    | 10'    | **~60 phút** |

---

## 📚 Tài liệu tham khảo

| Tài liệu                                                       | Mô tả                              |
| -------------------------------------------------------------- | ---------------------------------- |
| [prompts-to-generate-agent.md](./prompts-to-generate-agent.md) | 40+ prompts sẵn dùng               |
| [validation-checklist.md](./validation-checklist.md)           | Kiểm tra .agent có đúng không      |
| [success-metrics.md](./success-metrics.md)                     | KPIs + Quick Test + Feedback Loop  |
| [tool-specific-configs.md](./tool-specific-configs.md)         | Cấu hình cho Cursor/Copilot/Claude |
| [prebuilt-templates/](./prebuilt-templates/)                   | Templates sẵn cho Next.js, NestJS  |
| [example-backend-api.md](./example-backend-api.md)             | Ví dụ Backend (Node.js)            |
| [example-frontend-web.md](./example-frontend-web.md)           | Ví dụ Frontend (React)             |

---

**🏠 Quay về trang chính:** [README.md](./README.md)
