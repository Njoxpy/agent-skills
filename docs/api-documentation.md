---
name: api documentation
description: Production-grade API documentation best practices.
---

# API Documentation

## Instructions

Follow this guide when creating and publishing API documentation.

1. **Set up the documentation environment**

```bash
python -m venv .venv
source .venv/bin/activate

pip install mkdocs-material
pip freeze > requirements.txt
pip install -r requirements.txt

mkdocs new .
mkdocs serve
mkdocs build
mkdocs gh-deploy --force
```

2. **Document every endpoint consistently**

For each API endpoint, include:

- **Method**: `GET`, `POST`, `PUT`/`PATCH`, `DELETE`
- **Path**: e.g. `/api/v1/users/{userId}`
- **Description**: what the endpoint does
- **Authentication**: required auth type and header format
- **Path parameters**: required dynamic values in the URL
- **Query parameters**: optional filters/pagination/sorting
- **Request headers**: required headers such as `Content-Type` and `Authorization`
- **Request body**: schema and example (if applicable)
- **Response**:
  - success status code and example body
  - error status codes and example error responses
- **cURL test command**: runnable command for quick validation

3. **Use clear status code coverage**

Document common responses such as:

- `200 OK` for successful reads/updates
- `201 Created` for successful creation
- `204 No Content` for successful deletion with no body
- `400 Bad Request` for validation issues
- `401 Unauthorized` for missing/invalid auth
- `403 Forbidden` for access denied
- `404 Not Found` for missing resources
- `409 Conflict` for duplicate/conflicting operations
- `500 Internal Server Error` for unexpected failures

4. **Keep examples production-oriented**

- Use realistic sample payloads
- Show both success and failure cases
- Keep field names and types consistent across docs
- Ensure cURL examples match the documented method/path/body exactly

---

## Example Endpoint Template

### Create User

- **Method**: `POST`
- **Path**: `/api/v1/users`
- **Description**: Creates a new user account.

#### Request Headers

- `Content-Type: application/json`
- `Authorization: Bearer <token>`

#### Request Body

```json
{
  "name": "Jane Doe",
  "email": "jane@example.com",
  "role": "admin"
}
```

#### cURL

```bash
curl -X POST "https://api.example.com/api/v1/users" \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Jane Doe",
    "email": "jane@example.com",
    "role": "admin"
  }'
```

#### Success Response (`201 Created`)

```json
{
  "id": "usr_12345",
  "name": "Jane Doe",
  "email": "jane@example.com",
  "role": "admin",
  "createdAt": "2026-04-25T10:00:00Z"
}
```

#### Error Response (`400 Bad Request`)

```json
{
  "error": "ValidationError",
  "message": "Email is required"
}
```