# Doc-Gen - API Documentation Generator Plugin

## Overview

Doc-Gen is a Claude Code plugin that automatically generates comprehensive API documentation from your codebase. It creates OpenAPI/Swagger specifications, JSDoc/TSDoc comments, API reference guides, and usage examples, keeping documentation in sync with your implementation.

## What It Does

This plugin transforms code into clear, maintainable documentation:

- **OpenAPI/Swagger Specifications**: Complete API specs with request/response schemas
- **Code Comments**: JSDoc, TSDoc, Javadoc, Python docstrings, GoDoc, Rustdoc
- **API Reference Guides**: Markdown documentation with examples
- **Authentication Guides**: OAuth, JWT, API key documentation
- **Interactive Docs**: Swagger UI and Redoc integration

Supports multiple API types:
- **REST APIs**: Express, Fastify, NestJS, FastAPI, Spring Boot
- **GraphQL**: Apollo, GraphQL schemas
- **Function Libraries**: Utility libraries and SDKs

## Installation

```bash
/plugin install https://github.com/mei28/claude-code/doc-gen
```

Or manually:
```bash
git clone https://github.com/mei28/claude-code
ln -s $(pwd)/claude-code/doc-gen ~/.claude/plugins/doc-gen
```

## Usage

Generate docs for recent API changes:
```
/doc-gen
```

Generate docs for specific files:
```
/doc-gen src/api/users.ts
```

Generate OpenAPI spec:
```
/doc-gen --openapi
```

Add JSDoc comments to code:
```
/doc-gen --jsdoc
```

The plugin will:
1. Detect API type and framework
2. Analyze API code structure
3. Extract endpoints and schemas
4. Generate comprehensive documentation
5. Optionally validate specs

## Example

**Before** - Undocumented API:
```typescript
export async function getUser(req: Request, res: Response) {
  const { id } = req.params;
  const user = await db.users.findUnique({ where: { id } });

  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }

  return res.json(user);
}
```

**After** - Comprehensive Documentation:

**1. JSDoc Comments Added**:
```typescript
/**
 * Get user by ID
 *
 * Retrieves a single user by their unique identifier.
 *
 * @param req - Express request object
 * @param req.params.id - User ID (UUID format)
 * @param res - Express response object
 *
 * @returns {Promise<Response>} User object or 404 error
 *
 * @example
 * // GET /api/users/123e4567-e89b-12d3-a456-426614174000
 * // Response: 200 OK
 * {
 *   "id": "123e4567-e89b-12d3-a456-426614174000",
 *   "email": "john@example.com",
 *   "name": "John Doe",
 *   "role": "user",
 *   "createdAt": "2024-01-15T10:30:00Z"
 * }
 *
 * @throws {404} User not found
 */
export async function getUser(req: Request, res: Response) {
  const { id } = req.params;
  const user = await db.users.findUnique({ where: { id } });

  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }

  return res.json(user);
}
```

**2. OpenAPI Specification Generated** (`docs/openapi.yaml`):
```yaml
openapi: 3.0.0
info:
  title: User Management API
  version: 1.0.0

paths:
  /api/users/{id}:
    get:
      summary: Get user by ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
            format: uuid
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '404':
          description: User not found
```

**3. Markdown API Reference** (`docs/API.md`):
```markdown
## Get User by ID

**Endpoint**: `GET /api/users/{id}`

Retrieves a single user by their unique identifier.

**Parameters**:
| Name | Type | Required | Description |
|------|------|----------|-------------|
| id | string (UUID) | Yes | User unique identifier |

**Response** (200 OK):
```json
{
  "id": "123e4567-e89b-12d3-a456-426614174000",
  "email": "john@example.com",
  "name": "John Doe",
  "role": "user"
}
```

**Errors**:
- `404 Not Found`: User does not exist
```

## What Gets Generated

### Documentation Types
- ✅ OpenAPI/Swagger 3.0 specifications
- ✅ JSDoc/TSDoc code comments
- ✅ Markdown API references
- ✅ Request/response examples
- ✅ Error code documentation
- ✅ Authentication guides

### Code Comments
- ✅ Function descriptions
- ✅ Parameter documentation
- ✅ Return type specifications
- ✅ Error conditions
- ✅ Usage examples
- ✅ Links to related endpoints

### Integration
- ✅ Swagger UI setup code
- ✅ Redoc integration
- ✅ TypeScript type generation
- ✅ Client SDK examples

## Requirements

- Claude Code CLI
- API code to document
- Optional: OpenAPI validator (`@redocly/cli`)

## License

GPL-3.0

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
