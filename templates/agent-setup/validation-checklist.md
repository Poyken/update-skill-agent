# ✅ Validation Checklist - Kiểm tra `.agent` folder

> File này giúp bạn **tự động kiểm tra** xem thư mục `.agent` đã được setup đúng chưa.

---

## 🔍 Quick Validation (Chạy trong 2 phút)

### Bước 1: Chạy prompt này với AI

```
Hãy kiểm tra thư mục .agent/ trong dự án này và báo cáo:

1. **Files tồn tại:** Liệt kê tất cả files trong .agent/
2. **Files còn thiếu:** So sánh với cấu trúc chuẩn và liệt kê files thiếu
3. **Quality check cho mỗi file:**
   - Có evidence file không? (path đến code thật)
   - Có code examples không?
   - Có nội dung "lý thuyết suông" không? (should, best practice, recommended)
4. **Score:** Đánh giá 1-10 cho mỗi file

Output format:
| File | Tồn tại | Evidence | Examples | Lý thuyết suông | Score |
|------|---------|----------|----------|-----------------|-------|
```

### Bước 2: Kiểm tra kết quả

**Tiêu chuẩn PASS:**

- [ ] Tất cả Tier 1 files tồn tại (3 files)
- [ ] Mỗi file có ít nhất 1 evidence path
- [ ] Không có từ "should", "best practice", "recommended"
- [ ] Score trung bình ≥ 7/10

---

## 📋 Detailed Validation Checklist

### TIER 1 FILES (Bắt buộc)

#### ✅ `memory/project-context.md`

| Tiêu chí                             | Check | Ghi chú |
| ------------------------------------ | ----- | ------- |
| File tồn tại                         | □     |         |
| Có mô tả dự án (1-2 câu)             | □     |         |
| Có Tech Stack đầy đủ                 | □     |         |
| Có trạng thái features [x], [ ], [/] | □     |         |
| Có "Đang làm dở" section             | □     |         |
| Có "Bugs đã fix" ít nhất 1 entry     | □     |         |
| Có ngày cập nhật                     | □     |         |
| **Không có** nội dung generic        | □     |         |

**Validation Prompt:**

```
Đọc file .agent/memory/project-context.md và kiểm tra:
1. Có đúng là thông tin của DỰ ÁN NÀY không? (không phải template)
2. Tech Stack có khớp với package.json không?
3. Trạng thái features có đúng với code hiện tại không?
```

---

#### ✅ `rules/global.md`

| Tiêu chí                               | Check | Ghi chú |
| -------------------------------------- | ----- | ------- |
| File tồn tại                           | □     |         |
| Có ít nhất 5 categories                | □     |         |
| Mỗi rule có Evidence File              | □     |         |
| Mỗi rule có Code Example               | □     |         |
| **Không có** "should", "best practice" | □     |         |
| Naming conventions có ví dụ thực       | □     |         |
| Có bảng tổng hợp patterns              | □     |         |

**Validation Prompt:**

```
Đọc file .agent/rules/global.md và với MỖI rule:
1. Kiểm tra evidence file có tồn tại trong codebase không
2. Code example có đúng với file thật không
3. Báo cáo những rules không có evidence
```

---

#### ✅ `workflows/create-new-feature.md`

| Tiêu chí                        | Check | Ghi chú |
| ------------------------------- | ----- | ------- |
| File tồn tại                    | □     |         |
| Có folder structure cụ thể      | □     |         |
| Có commands thực tế (npm, git)  | □     |         |
| Có template code                | □     |         |
| Folder structure khớp với dự án | □     |         |
| Commands có thể chạy được       | □     |         |

**Validation Prompt:**

```
Đọc file .agent/workflows/create-new-feature.md và kiểm tra:
1. Folder structure có khớp với src/ hiện tại không?
2. Commands có đúng với package.json scripts không?
3. Template code có follow patterns trong rules/global.md không?
```

---

### TIER 2 FILES (Khuyến nghị)

#### ✅ `checklists/pr-review.md`

| Tiêu chí                                  | Check |
| ----------------------------------------- | ----- |
| Có ít nhất 10 items                       | □     |
| Items liên quan đến rules/global.md       | □     |
| Có priority levels (Critical/Major/Minor) | □     |

#### ✅ `rules/[domain].md`

| Tiêu chí                      | Check |
| ----------------------------- | ----- |
| Domain name phù hợp với dự án | □     |
| Rules cụ thể cho domain đó    | □     |
| Không duplicate với global.md | □     |

#### ✅ `skills/debug-skill.md`

| Tiêu chí                         | Check |
| -------------------------------- | ----- |
| Có trigger phrases               | □     |
| Có tools list từ devDependencies | □     |
| Có debug flow cho ≥3 loại bug    | □     |

---

## 🔴 Common Failures & Fixes

| Issue                   | Cách phát hiện                             | Cách sửa                              |
| ----------------------- | ------------------------------------------ | ------------------------------------- |
| **Generic content**     | Nội dung có thể apply cho bất kỳ dự án nào | Yêu cầu AI thêm evidence files cụ thể |
| **Missing evidence**    | Rules không có đường dẫn file              | Chạy Validation Prompt 9.1            |
| **Outdated info**       | Tech stack không khớp package.json         | Regenerate file với info mới          |
| **Copy-paste template** | Thấy [placeholder] chưa được thay          | Search `[` trong files và thay thế    |
| **Lý thuyết suông**     | Có "should", "recommended"                 | Chạy Prompt 10.3 để sửa               |

---

## 🎯 Scoring Guide

| Score    | Mô tả                                                    | Hành động                                  |
| -------- | -------------------------------------------------------- | ------------------------------------------ |
| **9-10** | Excellent. Mọi file đầy đủ, có evidence, không lý thuyết | Sử dụng ngay!                              |
| **7-8**  | Good. Có một số thiếu sót nhỏ                            | Sửa minor issues                           |
| **5-6**  | Average. Thiếu evidence hoặc có lý thuyết                | Chạy lại prompts với stricter requirements |
| **3-4**  | Poor. Nhiều file generic                                 | Cần regenerate từ đầu                      |
| **1-2**  | Fail. Hầu hết là template/lý thuyết                      | Xóa và làm lại                             |

---

## 🔄 Auto-Validation Script (Cho developer)

Nếu bạn muốn tự động hóa việc validation, tạo file này:

```bash
#!/bin/bash
# validate-agent.sh

echo "🔍 Validating .agent folder..."

# Check Tier 1 files exist
TIER1_FILES=(
  ".agent/memory/project-context.md"
  ".agent/rules/global.md"
  ".agent/workflows/create-new-feature.md"
)

for file in "${TIER1_FILES[@]}"; do
  if [ -f "$file" ]; then
    echo "✅ $file exists"

    # Check for "should", "best practice"
    if grep -qi "should\|best practice\|recommended" "$file"; then
      echo "⚠️  $file contains theory words!"
    fi

    # Check for evidence files
    if grep -q "src/" "$file"; then
      echo "✅ $file has evidence paths"
    else
      echo "⚠️  $file missing evidence paths!"
    fi
  else
    echo "❌ $file NOT FOUND"
  fi
done

echo ""
echo "🏁 Validation complete!"
```

**Chạy:**

```bash
chmod +x validate-agent.sh
./validate-agent.sh
```

---

**← Quay lại:** [Hướng dẫn vận hành](./operation-guide.md)
