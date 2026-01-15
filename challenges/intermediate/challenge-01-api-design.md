# Challenge 1: Design REST API

## 🎯 Objective

Use AI to design a complete REST API for a blog platform.

## Difficulty: ⭐⭐ Intermediate

---

## The Scenario

You're building a blog platform API. Use AI to design the complete API specification.

### Requirements

**Resources:**

- Users (auth, profiles)
- Posts (CRUD, drafts, published)
- Comments (nested)
- Categories
- Tags

**Features:**

- Authentication (JWT)
- Pagination for lists
- Search posts
- Filter by category/tag/author
- Like/unlike posts

---

## Your Task

Use AI to:

1. **Design API endpoints** - All routes with methods
2. **Define data models** - Request/response schemas
3. **Create database schema** - Tables and relationships
4. **Define error responses** - Standard error format
5. **Plan authentication flow** - Login, register, protected routes

---

## Deliverables

### Part 1: API Specification

Create endpoint documentation for all resources.

### Part 2: Database Schema

PostgreSQL schema with relationships.

### Part 3: Sample Implementation

Pick one resource and implement fully.

---

## Success Criteria

- [ ] RESTful endpoint naming
- [ ] Proper HTTP methods
- [ ] Consistent response format
- [ ] Pagination implemented
- [ ] Authentication documented
- [ ] Error handling defined
- [ ] Database normalized

---

## Evaluation Rubric

| Criteria                                 | Points |
| ---------------------------------------- | ------ |
| Endpoint design follows REST conventions | 20     |
| Complete CRUD for all resources          | 20     |
| Proper authentication design             | 15     |
| Error handling comprehensive             | 15     |
| Database schema normalized               | 15     |
| Code quality of implementation           | 15     |

---

## Hints

<details>
<summary>Hint 1: Start with design</summary>

```
"Design REST API endpoints for a blog platform.

Resources: Users, Posts, Comments, Categories

For each endpoint provide:
- Method + Path
- Description
- Auth required?
- Request body (if any)
- Response format
- Possible errors

Follow REST conventions."
```

</details>

<details>
<summary>Hint 2: Nested resources</summary>

For comments on posts:

```
GET /posts/:postId/comments
POST /posts/:postId/comments
```

</details>

<details>
<summary>Hint 3: Pagination format</summary>

```json
{
  "data": [...],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 100,
    "totalPages": 10
  }
}
```

</details>

---

## Reflection Questions

1. How did you structure prompts for API design?
2. What considerations did AI miss?
3. How did you handle nested resources?
4. What would you change for v2 of the API?

---

**Next →** [Challenge 2: Optimize Performance](./challenge-02-optimize.md)
