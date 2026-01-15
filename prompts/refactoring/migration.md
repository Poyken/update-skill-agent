# Migration Prompts

## 1. Library/Framework Migration

```
Help me migrate from [old library] to [new library]:

Current code using [old library]:
[paste code]

Requirements:
- Maintain same functionality
- [new library] version: [version]
- TypeScript support needed: [yes/no]

Provide:
1. Dependency changes
2. Code migration
3. Breaking changes to watch for
4. Testing approach
```

### Ví dụ:

```
Help me migrate from Moment.js to date-fns:

Current code:
import moment from 'moment';

function formatDate(date) {
  return moment(date).format('YYYY-MM-DD');
}

function addDays(date, days) {
  return moment(date).add(days, 'days').toDate();
}

function diffInDays(date1, date2) {
  return moment(date1).diff(moment(date2), 'days');
}

Migrate to date-fns v3.
```

---

## 2. Version Upgrade

```
Upgrade [framework] from [old version] to [new version]:

Current code:
[paste code with old patterns]

Help me:
1. Identify deprecated features used
2. Show new recommended patterns
3. Migrate code step by step
4. Handle breaking changes
```

---

## 3. Database Migration

```
Migrate database schema:

From:
[paste current schema]

To:
[describe desired changes]

Generate:
1. Migration script
2. Rollback script
3. Data transformation if needed
4. Zero-downtime migration strategy
```

---

## 4. API Version Migration

```
Migrate from API v[old] to v[new]:

Current integration:
[paste current API usage]

API changes:
[paste changelog or describe changes]

Update code to use new API while:
- Handling deprecation warnings
- Updating types/interfaces
- Testing edge cases
```

---

## 5. Architecture Migration

```
Help migrate from [old architecture] to [new architecture]:

Current structure:
[describe or paste current setup]

Target:
[describe desired architecture]

Provide:
1. Step-by-step migration plan
2. Code changes for each step
3. How to migrate incrementally
4. Rollback strategy
```

### Ví dụ:

```
Help migrate from monolith to microservices:

Current: Single Express.js app with:
- User authentication
- Product catalog
- Order management
- Payment processing

Target: Separate services for each domain

Provide incremental migration plan.
```
