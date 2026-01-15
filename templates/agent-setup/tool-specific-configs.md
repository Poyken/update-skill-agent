# ⚙️ Tool-Specific Configs - Cấu hình cho từng AI Tool

> Mỗi AI tool có cách đọc `.agent` folder khác nhau. File này hướng dẫn cách tối ưu cho từng tool.

---

## 📊 So sánh các AI Tools

| Feature                | Cursor        | GitHub Copilot        | Claude (Anthropic)  | ChatGPT             |
| ---------------------- | ------------- | --------------------- | ------------------- | ------------------- |
| **Đọc folder tự động** | ✅ `.cursor/` | ✅ `.github/copilot/` | ❌ Cần paste manual | ❌ Cần paste manual |
| **Context window**     | ~100K tokens  | ~8K tokens            | ~200K tokens        | ~128K tokens        |
| **File access**        | Full codebase | Limited               | No direct access    | No direct access    |
| **Best for**           | Daily coding  | Quick completions     | Complex analysis    | General tasks       |

---

## 🖥️ Cursor

### Cấu trúc folder được đọc tự động:

```
your-project/
├── .cursor/
│   └── rules/
│       └── rules.md     # Cursor đọc file này tự động
└── .agent/              # Cũng có thể dùng song song
```

### Cách setup:

**Bước 1:** Tạo `.cursor/rules/rules.md`

```markdown
# Project Rules for Cursor

## Quick Context

[Copy nội dung từ .agent/memory/project-context.md]

## Coding Rules

[Copy nội dung từ .agent/rules/global.md]

## When Creating New Features

[Copy nội dung từ .agent/workflows/create-new-feature.md]
```

**Bước 2:** Cấu hình Cursor Settings

Vào `Settings > Features > Docs`:

- Enable "Include .cursor rules"
- Add project-specific documentation

**Bước 3:** Test

Prompt: "Tạo một component mới theo rules của dự án"
→ Cursor sẽ tự động follow rules trong `.cursor/rules/rules.md`

### Tips cho Cursor:

- Giữ `rules.md` dưới 5000 từ (Cursor có limit)
- Đặt rules quan trọng nhất ở đầu file
- Dùng format đơn giản, tránh nested lists quá sâu

---

## 🤖 GitHub Copilot

### Cấu trúc folder được đọc:

```
your-project/
├── .github/
│   └── copilot/
│       └── instructions.md  # Copilot đọc file này
└── .agent/
```

### Cách setup:

**Bước 1:** Tạo `.github/copilot/instructions.md`

````markdown
# Copilot Instructions for [Project Name]

## Tech Stack

- Frontend: Next.js 14, TypeScript, TailwindCSS
- State: Zustand + React Query
- Testing: Jest + React Testing Library

## Coding Conventions

1. Components: PascalCase, trong src/components/
2. Hooks: useXxx, trong src/hooks/
3. Types: Định nghĩa trong types.ts cùng folder

## Do NOT

- Use 'any' type
- Use inline styles
- Import from relative paths beyond 2 levels (../../)

## Patterns

### Component Template

```tsx
interface Props {}
export function ComponentName({}: Props) {}
```
````

### Hook Template

```tsx
export function useHookName() {
  return useQuery({...})
}
```

````

**Bước 2:** Enable trong VS Code

Settings > Extensions > GitHub Copilot:
- Enable "Use Instruction Files"

**Bước 3:** Test

Type comment: `// create a new user profile component`
→ Copilot sẽ generate theo instructions

### Tips cho Copilot:
- Copilot có context window nhỏ (~8K tokens)
- Chỉ include rules CẦN THIẾT NHẤT
- Dùng examples ngắn gọn
- Tránh long explanations

---

## 🧠 Claude (Anthropic)

### Cách sử dụng với Claude:

Claude không đọc folder tự động, nhưng có context window RẤT LỚN (200K tokens).

**Bước 1:** Tạo file `claude-context.md`

```markdown
# Project Context for Claude

[Paste toàn bộ nội dung từ:]
- .agent/memory/project-context.md
- .agent/rules/global.md
- .agent/rules/ui-components.md
- .agent/workflows/create-new-feature.md
- .agent/checklists/pr-review.md

[Và cả source code quan trọng nếu cần]
````

**Bước 2:** Bắt đầu mỗi session

```
Đây là context của dự án tôi đang làm:

[Paste nội dung claude-context.md]

---

Bây giờ hãy giúp tôi: [task của bạn]
```

**Bước 3:** Dùng Projects (nếu có Claude Pro)

Claude Pro cho phép tạo "Project" với persistent context:

1. Tạo Project mới
2. Upload các files từ `.agent/`
3. Claude sẽ nhớ context cho mọi conversation trong Project

### Tips cho Claude:

- Tận dụng context window lớn - paste nhiều context hơn
- Dùng format Markdown rõ ràng
- Có thể paste cả source code files để Claude hiểu better
- Dùng Projects để không phải paste context mỗi lần

---

## 💬 ChatGPT

### Cách sử dụng với ChatGPT:

**Option 1: Custom GPT (GPT Plus)**

1. Tạo Custom GPT
2. Upload các files từ `.agent/` vào Knowledge base
3. Viết Instructions:

```
You are a coding assistant for [Project Name].
Always follow the rules in the uploaded files.
When writing code, reference the patterns from rules/global.md.
```

**Option 2: Manual Context (Free)**

```
# Project Context

Tech Stack: [list]
Coding Rules: [summary of rules]
Current Task: [what you're working on]

---

Help me with: [task]
```

### Tips cho ChatGPT:

- Giữ context ngắn gọn (context window ~128K nhưng performance giảm với long context)
- Summarize rules thay vì copy toàn bộ
- Refresh context sau mỗi 10-15 messages

---

## 🔄 Sync Script giữa các tools

Nếu bạn dùng nhiều tools, tạo script để sync:

```bash
#!/bin/bash
# sync-agent-to-tools.sh

echo "📂 Syncing .agent to tool-specific folders..."

# Create directories
mkdir -p .cursor/rules
mkdir -p .github/copilot

# Sync to Cursor
cat .agent/memory/project-context.md > .cursor/rules/rules.md
echo -e "\n---\n" >> .cursor/rules/rules.md
cat .agent/rules/global.md >> .cursor/rules/rules.md

# Sync to Copilot (shorter version)
cat > .github/copilot/instructions.md << 'EOF'
# Project Instructions
EOF
head -50 .agent/rules/global.md >> .github/copilot/instructions.md

# Create Claude context file
cat .agent/memory/project-context.md > claude-context.md
cat .agent/rules/global.md >> claude-context.md
cat .agent/workflows/create-new-feature.md >> claude-context.md

echo "✅ Sync complete!"
echo "- .cursor/rules/rules.md"
echo "- .github/copilot/instructions.md"
echo "- claude-context.md"
```

**Chạy sau mỗi lần update `.agent/`:**

```bash
chmod +x sync-agent-to-tools.sh
./sync-agent-to-tools.sh
```

---

## 📋 Recommendations theo Use Case

| Use Case                    | Best Tool | Lý do                               |
| --------------------------- | --------- | ----------------------------------- |
| **Daily coding**            | Cursor    | Auto-read rules, inline completions |
| **Quick fixes**             | Copilot   | Fast, integrated in editor          |
| **Architecture discussion** | Claude    | Large context, good reasoning       |
| **Code review**             | Claude    | Can analyze entire PR               |
| **Learning/explain code**   | ChatGPT   | Good explanations                   |
| **Refactoring large files** | Claude    | Can hold entire file in context     |

---

**← Quay lại:** [Hướng dẫn vận hành](./operation-guide.md)
