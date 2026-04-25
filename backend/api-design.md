---
name: api design
description: Production-grade API design best practices.
---

# API Design

## Instructions

Follow these rules when designing REST APIs:

1. **Version your APIs**
   - Use explicit versions like `/api/v1` or `/api/v2`.

2. **Use nouns, not verbs, in resource paths**
   - Good: `/api/v1/users`
   - Bad: `/api/v1/get-users`

3. **Use `/` to represent hierarchy**
   - Example: `/api/v1/users/{id}/orders`

4. **Do not use a trailing slash**
   - Good: `/api/v1/users`
   - Bad: `/api/v1/users/`

5. **Use hyphens (`-`) for readability**
   - Good: `/api/v1/blog-posts`

6. **Do not use underscores (`_`) in URIs**
   - Bad: `/api/v1/blog_posts`

7. **Use lowercase URI paths**
   - Good: `/api/v1/blogs/how-to-build-agents`
   - Bad: `/api/v1/blogs/How-To-Build-Agents`

8. **Do not include file extensions in URIs**
   - Bad: `/api/v1/users.json`

9. **Use consistent API subdomains**
   - Example: `api.example.com`

10. **Use a consistent developer portal subdomain**
   - Example: `developers.example.com`

11. **Use singular nouns for document resources**
   - Example: `/api/v1/user/{id}`

12. **Use plural nouns for collections**
   - Example: `/api/v1/users`

13. **Use plural nouns for stores**
   - Example: `/api/v1/orders`

14. **Use verbs or verb phrases for controller names (internal code), not URIs**
   - Example controller: `createUser`, `listUsers`

15. **Use identity-based values in variable path segments**
   - Example: `/api/v1/users/{userId}`

16. **Do not include CRUD verbs in URIs**
   - Bad: `/api/v1/create-user`
   - Good: `/api/v1/users`

## Examples

```js
// Versioning
app.use("/api/", route)   // Bad
app.use("/api/v1", route) // Good

// Nouns instead of verbs
"/api/v1/get-users" // Bad
"/api/v1/users"    // Good

// Hierarchical resource paths
"/api/v1/users/:id" // Good

// Hyphens for readability
"/api/v1/blogs/this-is-my-first-blog-post" // Good

// Underscores should not be used
"/api/v1/blogs/this_is_my_first_blog_post" // Bad

// Lowercase paths
"api.example.com/blogs/how-to-build-agents" // Good
"api.example.com/blogs/How-To-Build-Agents" // Bad
```
