# Test Improvement Prompts

## 1. Increase Test Coverage

```
Analyze this code and suggest missing tests:

[paste code]

Current tests:
[paste existing tests or describe coverage]

Identify:
1. Uncovered code paths
2. Missing edge cases
3. Untested error scenarios
4. Boundary conditions not tested

Generate the missing tests.
```

---

## 2. Fix Flaky Tests

```
This test is flaky (passes sometimes, fails sometimes):

[paste flaky test]

Failure pattern:
- Fails approximately [frequency]
- Error message: [message]
- Environment: [CI/local]

Diagnose the issue and fix it.
Common causes to check:
- Timing/race conditions
- Shared state between tests
- External dependencies
- Date/time dependencies
```

---

## 3. Improve Test Performance

```
These tests are slow:

[paste tests or describe]

Current execution time: [time]
Target time: [target]

Optimize by:
1. Reducing unnecessary setup
2. Parallelizing where possible
3. Using more efficient assertions
4. Mocking expensive operations
```

---

## 4. Test Refactoring

```
Refactor these tests for better maintainability:

[paste tests]

Problems:
- [issue 1]
- [issue 2]

Apply:
- DRY principle (extract common setup)
- Better test descriptions
- Page object pattern (for E2E)
- Custom assertions/matchers
```

---

## 5. Mock Improvement

```
Improve mocks in these tests:

[paste tests with mocks]

Issues:
- [describe mock problems]

Goals:
- More realistic mocks
- Easier to maintain
- Type-safe mocks
- Reusable mock factories
```
