# Anti-Patterns to Avoid

## 🎯 Purpose

Common mistakes that lead to poor AI outputs. Learn to recognize and avoid them.

---

## Anti-Pattern 1: Vague Requests ❌

### The Problem

```
❌ "Make it better"
❌ "Fix the bug"
❌ "Optimize this"
```

AI doesn't know what "better" means to you.

### The Fix

```
✅ "Make error messages more user-friendly.
   Instead of 'Validation error', show 'Please enter a valid email address'"

✅ "Fix the bug where form data resets after failed submit.
   Error: [paste error]
   Current behavior: [describe]
   Expected: [describe]"

✅ "Optimize database query for faster response:
   Current: 2 seconds
   Target: < 200ms
   Bottleneck seems to be the JOIN operation"
```

---

## Anti-Pattern 2: No Context ❌

### The Problem

```
❌ "How do I do authentication?"
❌ "What's wrong with my code?" (no code provided)
❌ "Best way to store data?"
```

### The Fix

```
✅ "How do I implement authentication in:
   - React 18 frontend
   - Express.js backend
   - PostgreSQL database
   Using JWT tokens with refresh token flow"

✅ "What's wrong here:
   [paste code]
   Error: [paste error]
   I expected: [expected behavior]"
```

---

## Anti-Pattern 3: Mega Prompts ❌

### The Problem

```
❌ "Build me a complete e-commerce platform with:
   - User auth with OAuth, email/password, 2FA
   - Product catalog with categories, variants, inventory
   - Shopping cart with guest checkout
   - Payment processing with Stripe
   - Order management with status tracking
   - Admin dashboard with analytics
   - Email notifications
   - Mobile responsive design
   - SEO optimization
   - ..."
```

Too much → AI can't do everything well.

### The Fix

Break into focused prompts:

```
✅ "Design the database schema for product catalog:
   - Products with title, description, price
   - Categories (hierarchical)
   - Variants (size, color)
   - Inventory tracking"

[next prompt]
✅ "Implement product CRUD API based on this schema..."

[next prompt]
✅ "Now implement category management..."
```

---

## Anti-Pattern 4: Blind Trust ❌

### The Problem

- Copying code without reading it
- Skipping code review
- Not testing generated code
- Assuming AI is always right

### The Risks

- Bugs in production
- Security vulnerabilities
- Inconsistent with project style
- May not handle edge cases

### The Fix

Always:

- [ ] Read and understand the code
- [ ] Check for your project conventions
- [ ] Test with various inputs
- [ ] Review for security issues
- [ ] Question assumptions

---

## Anti-Pattern 5: Ignoring Errors ❌

### The Problem

```
❌ "It gave me an error"
❌ "Something's not working"
❌ "I get a weird message"
```

### The Fix

```
✅ "I get this error:

TypeError: Cannot read properties of undefined (reading 'map')
    at UserList (UserList.tsx:15)
    at renderWithHooks (react-dom.development.js:14985)

When: Loading user list from API
Code: [paste relevant code]"
```

Always include:

- Full error message
- Stack trace
- What you were doing
- Relevant code

---

## Anti-Pattern 6: Prompt Repetition ❌

### The Problem

Asking the same question hoping for different answer.

```
Prompt: "Create a login form"
[AI gives answer]
Prompt: "Create a login form" (again)
[AI gives similar answer]
Prompt: "Create a login form, please this time make it good"
```

### The Fix

Give specific feedback:

```
✅ "The login form you provided works, but:
1. Error messages are too technical
2. Missing 'show password' toggle
3. Need to add 'remember me' checkbox

Please update with these additions."
```

---

## Anti-Pattern 7: Sharing Sensitive Data ❌

### The Problem

```
❌ Pasting code with API keys
❌ Including database credentials
❌ Sharing private business logic
❌ Production data in examples
```

### The Fix

```
✅ Replace with placeholders:
   - API_KEY="your_api_key_here"
   - DATABASE_URL="postgresql://user:pass@localhost/db"

✅ Use mock data:
   - user@example.com instead of real emails
   - Fake credit card numbers

✅ Anonymize business logic:
   - "Calculate discount based on rules" vs actual algorithm
```

---

## Anti-Pattern 8: All-or-Nothing ❌

### The Problem

- Rejecting entire response if one part is wrong
- Starting over instead of iterating
- Not using helpful parts

### The Fix

```
✅ "The structure is good, but:
   - Line 15: This won't work because [reason]
   - The validation logic is too simple

Keep the rest, fix these specific issues."
```

---

## Self-Check Checklist

Before sending a prompt:

- [ ] Is my request specific (not vague)?
- [ ] Did I include enough context?
- [ ] Am I asking for one thing (not mega prompt)?
- [ ] No sensitive data included?
- [ ] Did I include error messages if debugging?

Before applying AI's code:

- [ ] Did I read and understand it?
- [ ] Does it match project conventions?
- [ ] Is error handling present?
- [ ] Did I test it?
- [ ] No security issues?

---

**Related:** [Effective Patterns](./effective-patterns.md)
