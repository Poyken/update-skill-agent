# 📊 Success Metrics - Đo lường hiệu quả của `.agent`

> Làm sao biết `.agent` folder đang hoạt động tốt? File này định nghĩa các metrics và cách đo lường.

---

## 🎯 KPIs chính

### 1. First-Prompt Success Rate (FPSR)

**Định nghĩa:** Tỷ lệ AI trả lời đúng/đủ ngay từ prompt đầu tiên

**Cách đo:**

```
FPSR = (Số lần AI output đúng từ lần đầu) / (Tổng số prompts) × 100%
```

**Benchmarks:**
| FPSR | Đánh giá | Hành động |
|------|----------|-----------|
| 80-100% | Excellent | Maintain |
| 60-79% | Good | Minor improvements |
| 40-59% | Average | Review rules, thêm examples |
| < 40% | Poor | Regenerate .agent |

**Cách track:**
Sau mỗi session, ghi lại:

- [ ] AI hiểu context ngay? (Yes/No)
- [ ] AI follow đúng coding conventions? (Yes/No)
- [ ] Code AI viết có thể dùng ngay? (Yes/No)

---

### 2. Context Retention Rate (CRR)

**Định nghĩa:** AI có nhớ context từ `.agent` không?

**Cách test:**

```
Prompt: "Dự án này dùng state management gì? Kể 3 rules quan trọng nhất."

Expected: AI trả lời đúng theo .agent/rules/
```

**Benchmarks:**

- ✅ AI đọc được 5/5 thông tin chính = Excellent
- ⚠️ AI đọc được 3-4/5 = Good
- ❌ AI đọc được < 3/5 = Cần improve

---

### 3. Code Consistency Score (CCS)

**Định nghĩa:** Code AI generate có follow rules không?

**Cách đo thủ công (sau 1 tuần):**

```
Review 10 code snippets AI đã generate:
- Đúng naming conventions: _/10
- Đúng file structure: _/10
- Đúng patterns (hooks, error handling): _/10
- Có evidence từ rules: _/10

CCS = Tổng / 40 × 100%
```

---

### 4. Iteration Count (IC)

**Định nghĩa:** Số lần phải yêu cầu AI sửa lại

**Benchmarks:**
| Avg Iterations | Đánh giá |
|----------------|----------|
| 1-2 | Excellent - AI hiểu ngay |
| 3-4 | Good - Normal refinement |
| 5+ | Poor - Rules không clear |

---

## 📈 Tracking Template

### Daily Log (Tuỳ chọn)

```markdown
# AI Session Log - [DATE]

## Session 1

- **Task:** [Mô tả task]
- **First prompt success?** Yes/No
- **Iterations:** [số lần sửa]
- **AI followed rules?** Yes/Partially/No
- **Notes:** [ghi chú]

## Session 2

...

## Daily Summary

- Total prompts: X
- FPSR: X%
- Avg iterations: X
```

### Weekly Summary

```markdown
# Week [X] Summary

| Metric         | Value | Target | Status |
| -------------- | ----- | ------ | ------ |
| FPSR           | X%    | 70%    | ✅/❌  |
| Avg Iterations | X     | < 3    | ✅/❌  |
| Rules followed | X%    | 80%    | ✅/❌  |

## Improvements needed:

- [ ] ...
```

---

## 🧪 Quick Test Prompts

### Test 1: Context Check (1 phút)

```
Không nhìn vào bất kỳ file nào, chỉ dựa vào .agent folder, hãy trả lời:
1. Dự án này dùng framework gì?
2. State management dùng gì?
3. Naming convention cho components là gì?
4. Khi tạo feature mới, cần tạo những files gì?
```

**Scoring:**

- 4/4 đúng = ✅ Excellent
- 3/4 đúng = ⚠️ Good
- < 3/4 = ❌ Cần cải thiện context

---

### Test 2: Rule Compliance (2 phút)

```
Hãy tạo một component UserCard đơn giản với:
- Props: user object với name, email, avatar
- Có loading state
- Có error handling

Đảm bảo follow đúng mọi rules trong .agent/rules/
```

**Check list:**

- [ ] Đúng naming: UserCard (PascalCase)
- [ ] Đúng file location theo rules
- [ ] Đúng props pattern (interface/type)
- [ ] Đúng styling approach (Tailwind/CSS Modules)
- [ ] Có TypeScript types
- [ ] Follow error handling pattern

---

### Test 3: Workflow Knowledge (1 phút)

```
Tôi muốn thêm feature "Payment Integration".
Hãy liệt kê các bước và files cần tạo theo workflow của dự án.
```

**Expected:** AI respond theo `.agent/workflows/create-new-feature.md`

---

## 🔄 Feedback Loop: Cải thiện liên tục

### Khi AI làm sai:

```
AI vừa tạo code không đúng convention.

**Sai:** [mô tả cái sai]
**Đúng theo rules:** [đúng là gì]
**Evidence:** [file nào chứng minh]

Hãy:
1. Sửa lại code
2. Ghi nhớ rule này cho các lần sau
```

### Khi phát hiện rule thiếu:

```bash
# Thêm vào .agent/memory/project-context.md

## 🐛 Bugs/Issues phát hiện gần đây

### [DATE] - AI không biết về [X]
- **Vấn đề:** AI tạo code kiểu Y nhưng dự án dùng kiểu Z
- **Đã thêm rule:** Thêm vào rules/global.md section [X]
```

### Monthly Review Process:

1. **Collect data:** Xem lại session logs
2. **Identify patterns:** AI thường sai ở đâu?
3. **Update rules:** Thêm/sửa rules thiếu
4. **Test lại:** Chạy Quick Test Prompts
5. **Document:** Ghi lại trong memory/project-context.md

---

## 📉 Warning Signs (Dấu hiệu cần improve)

| Warning Sign                       | Khả năng nguyên nhân   | Hành động                    |
| ---------------------------------- | ---------------------- | ---------------------------- |
| AI hay hỏi lại "Bạn dùng X hay Y?" | Rules không rõ ràng    | Thêm specific info vào rules |
| Code AI viết không consistent      | Thiếu examples         | Thêm code examples           |
| AI bỏ qua một số rules             | Rules quá nhiều/dài    | Tách thành nhiều files nhỏ   |
| AI viết lý thuyết thay vì code     | Context chưa được load | Paste lại context            |
| Phải sửa đi sửa lại                | Rules mâu thuẫn        | Review và consolidate rules  |

---

## 🏆 Success Indicators

Bạn biết `.agent` đang work khi:

✅ AI tạo code đúng convention ngay lần đầu
✅ AI biết folder structure mà không cần hỏi
✅ AI reference đến patterns trong codebase
✅ AI nhắc bạn khi code của bạn vi phạm rules
✅ Code AI viết có thể merge mà chỉ cần minor edits
✅ Thời gian onboard dev mới giảm (họ đọc .agent thay vì hỏi)

---

**← Quay lại:** [Hướng dẫn vận hành](./operation-guide.md)
