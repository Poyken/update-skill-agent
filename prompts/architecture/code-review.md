# Code Review Prompts

## 1. Security Review

```
Review this code for security vulnerabilities:

[paste code]

Check for:
1. Injection attacks (SQL, XSS, Command)
2. Authentication/authorization flaws
3. Sensitive data exposure
4. Insecure dependencies
5. CSRF vulnerabilities
6. Input validation issues

For each issue found:
- Severity: High/Medium/Low
- Location: [file:line]
- Description: What's wrong
- Fix: How to fix it
```

---

## 2. Performance Review

```
Review this code for performance:

[paste code]

Context:
- Expected load: [describe]
- Current issues: [if any]

Analyze:
1. Time complexity
2. Memory usage
3. Database queries (N+1, etc)
4. Unnecessary operations
5. Caching opportunities
6. Async/parallel optimization

Prioritize recommendations by impact.
```

---

## 3. Code Quality Review

```
Review code quality:

[paste code]

Standards: [coding standards if any]

Evaluate:
1. Readability
2. Maintainability
3. SOLID principles adherence
4. Error handling
5. Documentation
6. Test coverage

Provide specific actionable feedback.
```

---

## 4. PR Review

```
Review this pull request:

Changes:
[paste diff or describe changes]

PR description:
[paste PR description]

Check:
1. Does it solve the stated problem?
2. Code quality and style
3. Test coverage
4. Performance implications
5. Security considerations
6. Breaking changes
7. Documentation updates needed

Provide review comments.
```
