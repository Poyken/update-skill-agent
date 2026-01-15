# Quy chuẩn Code (Coding Conventions)

## Naming Conventions

| Loại            | Quy tắc             | Ví dụ                     |
| --------------- | ------------------- | ------------------------- |
| Components      | PascalCase          | `UserProfile.tsx`         |
| Hooks           | camelCase + `use`   | `useAuth.ts`              |
| Utils/Helpers   | camelCase           | `formatDate.ts`           |
| Constants       | UPPER_SNAKE_CASE    | `API_BASE_URL`            |
| Types/Interface | PascalCase + suffix | `UserDto`, `AuthResponse` |
| Folders         | kebab-case          | `user-profile/`           |

---

## Cấu trúc Component

Mỗi component phức tạp nên có cấu trúc folder riêng:

```
ComponentName/
├── index.tsx              # Component chính (export default)
├── ComponentName.test.tsx # Unit tests
├── types.ts               # TypeScript interfaces (nếu cần)
└── hooks.ts               # Hooks riêng của component (nếu cần)
```

---

## TypeScript Rules

- ❌ Không dùng `any`. Nếu không biết type, dùng `unknown` và narrow down.
- ✅ Dùng `interface` cho object shapes, `type` cho unions/intersections.
- ✅ Export types từ file riêng (`types.ts`) trong mỗi feature.

```typescript
// ✅ Good
interface User {
  id: string;
  email: string;
  role: "admin" | "user";
}

// ❌ Bad
const user: any = fetchUser();
```

---

## Git Conventions

### Branch Naming

- `feature/ten-tinh-nang` - Tính năng mới
- `fix/ten-bug` - Sửa bug
- `refactor/ten-module` - Refactor code
- `chore/ten-task` - Cập nhật config, dependencies

### Commit Message (Conventional Commits)

```
<type>(<scope>): <subject>

Ví dụ:
feat(auth): add password reset functionality
fix(cart): resolve quantity update issue
refactor(api): migrate to axios from fetch
docs(readme): update installation guide
```

---

## Error Handling

Sử dụng custom `AppError` class thay vì throw Error trực tiếp:

```typescript
// src/lib/errors.ts
export class AppError extends Error {
  constructor(
    public message: string,
    public code: string,
    public statusCode: number = 400
  ) {
    super(message);
  }
}

// Sử dụng:
throw new AppError("User not found", "USER_NOT_FOUND", 404);
```

---

## Import Order

Sắp xếp imports theo thứ tự:

1. External packages (react, next, lodash...)
2. Internal aliases (@/components, @/hooks...)
3. Relative imports (./Component, ../utils)
4. Types (cuối cùng)

```typescript
// 1. External
import React, { useState } from "react";
import { useQuery } from "@tanstack/react-query";

// 2. Internal aliases
import { Button } from "@/components/ui";
import { useAuth } from "@/hooks";

// 3. Relative
import { formatDate } from "../utils";

// 4. Types
import type { User } from "./types";
```
