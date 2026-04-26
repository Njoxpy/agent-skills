---
name: api design
description: Production-grade REST API design conventions — naming, versioning, hierarchy, response shape, and resource modeling.
---

# API Design

Conventions for designing predictable, consistent REST APIs.

## Instructions

### 1. Versioning

Always version the API in the URL path. Unversioned public APIs cannot evolve safely.

```js
app.use("/api/", route);   // Bad — no version
app.use("/api/v1", route); // Good
```

- Use major versions only: `v1`, `v2` — not `v1.2`.
- Keep at least one prior version live during a migration window.

### 2. Resource naming

Resources are **nouns**. The HTTP method supplies the verb.

| Bad | Good |
|-----|------|
| `GET /api/v1/get-users` | `GET /api/v1/users` |
| `POST /api/v1/create-user` | `POST /api/v1/users` |
| `POST /api/v1/users/{id}/delete` | `DELETE /api/v1/users/{id}` |

#### Singular vs plural

| Resource type | Form | Example |
|---------------|------|---------|
| Collection | plural | `/api/v1/users` |
| Store | plural | `/api/v1/orders` |
| Single document | singular | `/api/v1/user/profile` |

### 3. Hierarchy

Use `/` to express parent/child relationships. Use **identity-based** values (`{userId}`, not `{userName}`) for path parameters.

```
/api/v1/users/{userId}
/api/v1/users/{userId}/orders
/api/v1/users/{userId}/orders/{orderId}
```

Avoid nesting more than two levels deep — flatten with query parameters or a top-level resource instead.

### 4. Path formatting

| Rule | Bad | Good |
|------|-----|------|
| Lowercase only | `/api/v1/BlogPosts` | `/api/v1/blog-posts` |
| Hyphens, not underscores | `/api/v1/blog_posts` | `/api/v1/blog-posts` |
| No trailing slash | `/api/v1/users/` | `/api/v1/users` |
| No file extensions | `/api/v1/users.json` | `/api/v1/users` |
| Readable slugs | `/api/v1/blogs/123` | `/api/v1/blogs/how-to-build-agents` |

### 5. Subdomains

| Purpose | Subdomain |
|---------|-----------|
| API traffic | `api.example.com` |
| Developer portal / docs | `developers.example.com` |

Keep these consistent across environments (`api.staging.example.com`, `api.example.com`).

### 6. HTTP methods

| Method | Use for |
|--------|---------|
| `GET` | Read a resource or collection (idempotent, no body) |
| `POST` | Create a new resource |
| `PUT` | Replace a resource entirely |
| `PATCH` | Partially update a resource |
| `DELETE` | Remove a resource |

### 7. Internal naming (controllers)

URIs use nouns; **code** uses verbs. Controller and handler names should clearly state the action.

```js
// Good — verbs in code, nouns in routes
router.get("/users",        listUsers);
router.post("/users",       createUser);
router.get("/users/:id",    getUser);
router.patch("/users/:id",  updateUser);
router.delete("/users/:id", deleteUser);
```

### 8. Query parameters

Use query params for filtering, sorting, and pagination — never to specify the resource itself.

```
GET /api/v1/users?role=admin&status=active   // Good — filtering
GET /api/v1/users?sort=createdAt&order=desc  // Good — sorting
GET /api/v1/users?page=2&limit=50            // Good — pagination
GET /api/v1/get-user?id=123                  // Bad — id belongs in the path
```

### 9. Consistent response structure

Every endpoint must return the same response envelope so clients can parse success, errors, and metadata uniformly.

#### Envelope

| Field | Purpose |
|-------|---------|
| `success` | Boolean — did the request succeed |
| `message` | Human-readable summary of the result |
| `data` | Payload (object, array, or `null`) |
| `errors` | Array of error details, or `null` on success |
| `meta` | Pagination/standardized metadata, or `null` |

#### Bad — raw array, no envelope

```json
[
  {
    "_id": "69ea48a881acf8883bad558f",
    "name": "Chakula kwa ajili ya kuku wadogo",
    "description": "chakula cha ngombwe ambao wamezaliwa",
    "quantity": 999,
    "nutrients": "vitamin",
    "createdAt": "2026-04-23T16:28:24.255Z",
    "updatedAt": "2026-04-25T13:15:38.742Z",
    "__v": 0
  }
]
```

#### Good — wrapped, with metadata

```json
{
  "success": true,
  "message": "Request completed successfully",
  "data": [
    {
      "_id": "69ea48a881acf8883bad558f",
      "name": "Chakula kwa ajili ya kuku wadogo",
      "description": "chakula cha ngombwe ambao wamezaliwa",
      "quantity": 999,
      "nutrients": "vitamin",
      "createdAt": "2026-04-23T16:28:24.255Z",
      "updatedAt": "2026-04-25T13:15:38.742Z",
      "__v": 0
    }
  ],
  "errors": null,
  "meta": {
    "page": 1,
    "total": 20
  }
}
```

#### Good — error response

```json
{
  "success": false,
  "message": "Validation failed",
  "data": null,
  "errors": [
    { "field": "email", "message": "Email is required" }
  ],
  "meta": null
}
```

## Quick reference

```
# Collections
GET    /api/v1/users
POST   /api/v1/users

# Single resource
GET    /api/v1/users/{userId}
PATCH  /api/v1/users/{userId}
DELETE /api/v1/users/{userId}

# Nested resources
GET    /api/v1/users/{userId}/orders
GET    /api/v1/users/{userId}/orders/{orderId}

# Filtering, sorting, pagination
GET    /api/v1/users?role=admin&sort=createdAt&order=desc&page=1&limit=50
```
