# 🔷 Next.js + TailwindCSS Template

> Pre-built `.agent` template cho dự án Next.js 14 (App Router) với TailwindCSS, TypeScript, React Query và Zustand.

---

## ⚡ Quick Setup

```bash
# 1. Tạo folder .agent
mkdir -p .agent/{memory,rules,workflows,checklists,skills}

# 2. Copy từng file bên dưới vào đúng vị trí
```

---

## 📁 FILE: `.agent/memory/project-context.md`

```markdown
# Project Memory - [PROJECT_NAME]

> Cập nhật: [DATE]

## Mô tả ngắn gọn

[1-2 câu mô tả dự án]

## Tech Stack

| Layer          | Công nghệ                    |
| -------------- | ---------------------------- |
| Framework      | Next.js 14 (App Router)      |
| Language       | TypeScript (Strict mode)     |
| Styling        | TailwindCSS                  |
| State - Client | Zustand                      |
| State - Server | React Query (TanStack Query) |
| Forms          | React Hook Form + Zod        |
| Testing        | Jest + React Testing Library |
| Linting        | ESLint + Prettier            |

## Cấu trúc thư mục
```

src/
├── app/ # Next.js App Router pages
│ ├── (auth)/ # Route group for auth pages
│ ├── (main)/ # Route group for main app
│ └── api/ # API routes
├── components/
│ ├── ui/ # Primitive components (Button, Input, Card)
│ └── features/ # Feature-specific components
├── hooks/ # Custom hooks
├── services/ # API client and external services
├── store/ # Zustand stores
├── lib/ # Utilities (cn, api-client)
├── types/ # TypeScript types
└── styles/ # Global styles

```

## Trạng thái hiện tại

- [x] Project setup (Next.js, TailwindCSS, TypeScript)
- [x] UI Component library (Button, Input, Card, Modal)
- [ ] Authentication
- [ ] [Feature 1]
- [ ] [Feature 2]

## 🔄 Đang làm dở

- **Feature:** [Current feature]
- **Branch:** feature/[branch-name]
- **Status:** [X]%
- **Next steps:** [What to do next]

## 🐛 Bugs đã fix (Lessons Learned)

### Bug #1: Hydration Mismatch
- **Triệu chứng:** Console warning về hydration
- **Nguyên nhân:** useState với Date.now() trong SSR
- **Cách fix:** Wrap trong useEffect hoặc dùng 'use client'
- **Bài học:** Luôn consider SSR khi dùng browser-specific APIs

## ⚠️ Quirks & Workarounds

- `'use client'` directive cần ở đầu file trước imports
- Next.js Image cần config domain whitelist trong `next.config.js`
- Zustand persist với SSR cần `skipHydration: true`
- TailwindCSS JIT cần đúng content paths trong config
```

---

## 📁 FILE: `.agent/rules/global.md`

```markdown
# Quy tắc Code Chung - [PROJECT_NAME]

> ⚠️ Các quy tắc này được rút ra từ code hiện có, KHÔNG phải lý thuyết.

## 1. Naming Conventions

| Loại       | Pattern            | Evidence                       |
| ---------- | ------------------ | ------------------------------ |
| Components | PascalCase         | `src/components/ui/Button.tsx` |
| Hooks      | camelCase + use    | `src/hooks/useAuth.ts`         |
| Stores     | camelCase + Store  | `src/store/cartStore.ts`       |
| Utils      | camelCase          | `src/lib/utils.ts`             |
| Types      | PascalCase         | `src/types/User.ts`            |
| Pages      | lowercase (folder) | `src/app/dashboard/page.tsx`   |

## 2. File Structure

### Components
```

ComponentName/
├── index.tsx # Main component, exports default
├── types.ts # TypeScript interfaces (if complex)
└── hooks.ts # Component-specific hooks (if any)

# OR for simple components:

ComponentName.tsx

```

### Features
```

src/features/[feature-name]/
├── components/ # Feature-specific components
├── hooks/ # Feature-specific hooks
├── types.ts # Feature types
└── index.ts # Public exports

````

## 3. TypeScript Rules

- ❌ KHÔNG dùng `any`. Dùng `unknown` nếu cần và narrow down
- ✅ Dùng `interface` cho object shapes
- ✅ Dùng `type` cho unions/aliases
- ✅ Export types từ file riêng

```typescript
// ✅ Good - từ src/types/User.ts
export interface User {
  id: string;
  email: string;
  name: string;
}

// ❌ Bad
const user: any = fetchUser();
````

## 4. Styling (TailwindCSS)

```tsx
// ✅ Dùng cn() helper cho conditional classes - từ src/lib/utils.ts
import { cn } from '@/lib/utils';

<button className={cn(
  'px-4 py-2 rounded-lg',
  variant === 'primary' && 'bg-blue-600 text-white',
  disabled && 'opacity-50 cursor-not-allowed'
)}>

// ❌ KHÔNG dùng inline styles
<button style={{ padding: '16px' }}>

// ✅ Responsive: Mobile-first
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4">
```

## 5. State Management

### Client State (Zustand)

```typescript
// từ src/store/cartStore.ts
import { create } from "zustand";
import { persist } from "zustand/middleware";

interface CartStore {
  items: CartItem[];
  addItem: (item: CartItem) => void;
}

export const useCartStore = create<CartStore>()(
  persist(
    (set) => ({
      items: [],
      addItem: (item) =>
        set((state) => ({
          items: [...state.items, item],
        })),
    }),
    { name: "cart-storage" }
  )
);
```

### Server State (React Query)

```typescript
// từ src/hooks/useProducts.ts
export function useProducts() {
  return useQuery({
    queryKey: ["products"],
    queryFn: productService.getAll,
    staleTime: 5 * 60 * 1000,
  });
}

export function useCreateProduct() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: productService.create,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ["products"] });
    },
  });
}
```

## 6. API Integration

```typescript
// ✅ Luôn qua service layer - từ src/services/product.service.ts
export const productService = {
  getAll: async (): Promise<Product[]> => {
    const res = await apiClient.get("/products");
    return res.data;
  },
  create: async (data: CreateProductDto): Promise<Product> => {
    const res = await apiClient.post("/products", data);
    return res.data;
  },
};

// ❌ KHÔNG fetch trực tiếp trong components
```

## 7. Import Order

```typescript
// 1. React/Next
import React, { useState, useEffect } from "react";
import { useRouter } from "next/navigation";

// 2. Third-party
import { useQuery } from "@tanstack/react-query";

// 3. Internal (absolute imports)
import { Button } from "@/components/ui";
import { useAuth } from "@/hooks/useAuth";

// 4. Relative
import { ProductCard } from "./ProductCard";

// 5. Types (last)
import type { Product } from "@/types";
```

## 8. Error Handling

```typescript
// React Query handles errors automatically
// For custom handling:
const { error, isError } = useQuery({...});

if (isError) {
  return <ErrorMessage error={error} />;
}

// API errors
try {
  await apiClient.post('/endpoint', data);
} catch (error) {
  if (error instanceof ApiError) {
    toast.error(error.message);
  }
}
```

````

---

## 📁 FILE: `.agent/rules/ui-components.md`

```markdown
# Quy tắc UI Components

## 1. Component Props

```tsx
// ✅ Interface riêng cho props
interface ButtonProps {
  children: React.ReactNode;
  variant?: 'primary' | 'secondary' | 'ghost';
  size?: 'sm' | 'md' | 'lg';
  isLoading?: boolean;
  disabled?: boolean;
  onClick?: () => void;
}

export function Button({
  children,
  variant = 'primary',
  size = 'md',
  isLoading = false,
  disabled = false,
  onClick
}: ButtonProps) {
  // ...
}
````

## 2. Loading States

```tsx
// Skeleton pattern
if (isLoading) {
  return <ComponentSkeleton />;
}

function ComponentSkeleton() {
  return (
    <div className="animate-pulse">
      <div className="bg-gray-200 h-4 rounded w-3/4" />
    </div>
  );
}
```

## 3. Forms (React Hook Form + Zod)

```tsx
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";

const schema = z.object({
  email: z.string().email("Invalid email"),
  password: z.string().min(8, "Min 8 characters"),
});

type FormData = z.infer<typeof schema>;

export function LoginForm() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<FormData>({
    resolver: zodResolver(schema),
  });

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Input {...register("email")} error={errors.email?.message} />
      <Button type="submit">Submit</Button>
    </form>
  );
}
```

## 4. Accessibility

- Tất cả Button/Input có accessible names
- Images có alt text
- Focus states visible
- Keyboard navigation works

````

---

## 📁 FILE: `.agent/workflows/create-new-feature.md`

```markdown
# Workflow: Tạo Feature Mới

## Bước 1: Tạo branch

```bash
git checkout main
git pull origin main
git checkout -b feature/[feature-name]
````

## Bước 2: Tạo folder structure

```bash
mkdir -p src/features/[feature-name]/{components,hooks}
touch src/features/[feature-name]/{index.ts,types.ts}
```

## Bước 3: Tạo types

```typescript
// src/features/[feature-name]/types.ts
export interface [FeatureName] {
  id: string;
  // ...
}

export interface [FeatureName]Props {
  // ...
}
```

## Bước 4: Tạo hook (nếu cần API)

```typescript
// src/features/[feature-name]/hooks/use[FeatureName].ts
import { useQuery } from '@tanstack/react-query';
import { [featureName]Service } from '@/services';

export function use[FeatureName]() {
  return useQuery({
    queryKey: ['[featureName]'],
    queryFn: [featureName]Service.getAll,
  });
}
```

## Bước 5: Tạo component

```tsx
// src/features/[feature-name]/components/[FeatureName].tsx
'use client';

import { use[FeatureName] } from '../hooks/use[FeatureName]';
import type { [FeatureName]Props } from '../types';

export function [FeatureName]({ }: [FeatureName]Props) {
  const { data, isLoading, error } = use[FeatureName]();

  if (isLoading) return <[FeatureName]Skeleton />;
  if (error) return <ErrorMessage error={error} />;

  return (
    <div>
      {/* content */}
    </div>
  );
}
```

## Bước 6: Export

```typescript
// src/features/[feature-name]/index.ts
export * from "./components/[FeatureName]";
export * from "./hooks/use[FeatureName]";
export type * from "./types";
```

## Bước 7: Tạo page (nếu cần)

```tsx
// src/app/[feature-name]/page.tsx
import { [FeatureName] } from '@/features/[feature-name]';

export default function [FeatureName]Page() {
  return <[FeatureName] />;
}
```

## Bước 8: Commit

```bash
git add .
git commit -m "feat([feature-name]): implement [feature-name]

- Add [FeatureName] component
- Add use[FeatureName] hook
- Add types"

git push origin feature/[feature-name]
```

````

---

## 📁 FILE: `.agent/checklists/pr-review.md`

```markdown
# PR Review Checklist

## Trước khi Review
- [ ] Branch đã rebase từ main
- [ ] Không có conflicts
- [ ] CI/CD passed

## Code Quality
- [ ] TypeScript strict - không có `any`
- [ ] Đúng naming conventions
- [ ] Import order đúng
- [ ] Không có console.log

## Components
- [ ] Có TypeScript interface cho props
- [ ] Có loading/error states
- [ ] Responsive (mobile-first)
- [ ] Accessible (alt, aria-labels)

## State
- [ ] Server state dùng React Query
- [ ] Client state dùng Zustand
- [ ] Mutations invalidate đúng queries

## Styles
- [ ] Dùng TailwindCSS, không inline styles
- [ ] Dùng cn() cho conditional classes
- [ ] Responsive breakpoints đúng

## Performance
- [ ] Images dùng next/image
- [ ] Có loading states (no layout shift)
- [ ] Large components có lazy loading
````

---

## 🎯 Sau khi copy

Chạy prompt này để customize:

```
Tôi đã copy Next.js + TailwindCSS template vào .agent/

Hãy đọc các files và CUSTOMIZE cho dự án hiện tại:
1. Quét package.json để verify tech stack
2. Quét src/ để cập nhật folder structure
3. Tìm 5 components thực tế để làm evidence cho rules
4. Cập nhật trạng thái features dựa trên code hiện có

Output từng file đã customized.
```

---

**← Quay lại:** [Pre-built Templates](./README.md)
