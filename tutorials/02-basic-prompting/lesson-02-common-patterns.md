# Lesson 2: Common Prompt Patterns

## 🎯 Mục tiêu

- Học các prompt patterns thường dùng
- Biết khi nào apply pattern nào
- Build library của bạn

---

## Pattern 1: Role Assignment

Gán role cho AI để get better context.

```
"Act as a senior React developer reviewing code for a junior developer.
Review this component and suggest improvements:
[paste code]"
```

```
"You are a security expert. Analyze this authentication code for vulnerabilities:
[paste code]"
```

**Khi dùng:** Code review, learning, getting expert perspective

---

## Pattern 2: Step-by-Step Request

Yêu cầu AI làm từng bước.

```
"Implement user registration:

Step 1: Create the API endpoint structure
Step 2: Add input validation
Step 3: Implement password hashing
Step 4: Save to database
Step 5: Send confirmation email

Show each step separately with explanations."
```

**Khi dùng:** Complex features, learning process, documentation

---

## Pattern 3: Example-Driven

Cho example về expected output.

```
"Convert these functions to TypeScript with proper types.

Example:
// Before
function greet(name) {
  return 'Hello ' + name;
}

// After
function greet(name: string): string {
  return `Hello ${name}`;
}

Now convert these:
[paste functions]"
```

**Khi dùng:** Formatting, consistent style, transformations

---

## Pattern 4: Comparison Request

Để AI so sánh options.

```
"Compare Redux Toolkit vs Zustand for state management:

Context: Medium-sized React app, 5-person team, need:
- Server state caching
- Optimistic updates
- DevTools support

Create a comparison table with pros/cons of each."
```

**Khi dùng:** Technology decisions, approach selection

---

## Pattern 5: Explain Then Implement

Yêu cầu giải thích trước khi code.

```
"I need to implement infinite scroll for a product list.

First, explain:
1. How infinite scroll works
2. Common approaches (intersection observer, scroll events)
3. Pros/cons of each

Then, implement using the best approach for React."
```

**Khi dùng:** Learning new concepts, understanding trade-offs

---

## Pattern 6: Rubber Duck Debugging

Dùng AI như rubber duck, explain problem.

```
"I'm debugging an issue. Let me explain what's happening:

What I expect: User clicks 'Save', form data saves to database
What happens: Nothing happens, no errors in console
What I've tried: Added console.log in submit handler - never fires

Here's my component:
[paste code]

As I explain this, does anything stand out as potentially wrong?"
```

**Khi dùng:** Debugging, when stuck, need fresh perspective

---

## Pattern 7: Constraint-First

Start with constraints để narrow solution space.

```
"I need a caching solution with these constraints:
- No Redis (budget constraint)
- Works in serverless environment
- Cache invalidation within 5 minutes
- Simple to implement

Given these constraints, what are my options?"
```

**Khi dùng:** Technology selection, architectural decisions

---

## Pattern 8: Iterative Refinement

Start simple, add complexity.

```
Iteration 1: "Create a basic user form with name and email"

Iteration 2: "Add validation - email format, name required"

Iteration 3: "Add loading state and error handling"

Iteration 4: "Add success toast notification"
```

**Khi dùng:** Complex features, exploring solutions

---

## Pattern 9: Test-First

Ask for tests before implementation.

```
"I need to implement a function calculateShipping(weight, destination)

First, write the unit tests covering:
- Normal cases
- Edge cases (0 weight, international)
- Error cases

Then implement the function to pass all tests."
```

**Khi dùng:** TDD approach, ensuring test coverage

---

## Pattern 10: Documentation-First

Ask for docs/types before code.

```
"I'm building a notification system.

First, design:
1. TypeScript interfaces for Notification types
2. API contract for CRUD operations
3. Database schema

Then implement based on these designs."
```

**Khi dùng:** Complex systems, team collaboration

---

## 📝 Exercises

### Exercise 1: Pattern matching

Cho mỗi scenario, chọn pattern phù hợp:

1. Học về WebSocket implementation
2. Chọn giữa MongoDB và PostgreSQL
3. Debug form không submit
4. Build dashboard từ đầu

### Exercise 2: Apply patterns

Với task hiện tại của bạn, thử apply 3 patterns khác nhau. So sánh kết quả.

---

## Pattern Cheat Sheet

| Pattern          | Use When         | Example Start                |
| ---------------- | ---------------- | ---------------------------- |
| Role Assignment  | Need expertise   | "Act as a..."                |
| Step-by-Step     | Complex features | "Step 1:..."                 |
| Example-Driven   | Transformations  | "Like this example..."       |
| Comparison       | Decisions        | "Compare X vs Y..."          |
| Explain First    | Learning         | "First explain, then..."     |
| Rubber Duck      | Debugging        | "Let me explain..."          |
| Constraint-First | Selection        | "Given these constraints..." |
| Iterative        | Building up      | "Start with basic..."        |
| Test-First       | TDD              | "First write tests..."       |
| Docs-First       | Architecture     | "First design..."            |

---

**← Previous:** [CLEAR Framework](./lesson-01-clear-framework.md)
**Next →** [Module 3: Advanced Techniques](../03-advanced-techniques/)
