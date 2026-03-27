---
name: api-contract
description: Create API contracts before implementation. Defines endpoints, request/response schemas, error codes. Prevents frontend/backend desync.
---

# API Contract

Define API contracts before implementing. Contract-first development prevents
the #1 cause of frontend/backend bugs: mismatched assumptions.

## Usage

`/appbuilder-one:api-contract [feature-name]` — Create contract for a feature
`/appbuilder-one:api-contract list` — List all contracts
`/appbuilder-one:api-contract verify` — Check implementation matches contracts

## Why Contract-First

Without contracts, frontend and backend often end up with:
- Different field names (`full_name` vs `first_name` + `last_name`)
- Different data formats (form-urlencoded vs JSON)
- Different response structures
- Unhandled error cases

## Workflow

### 1. Create Contract

For each endpoint, define:

```markdown
# API Contract: [Feature] — [Endpoint Name]

## Endpoint
- **Method**: POST
- **Path**: /api/v1/users
- **Auth**: Required (Bearer token)
- **Content-Type**: application/json

## Request

```json
{
  "email": "string (required, valid email)",
  "password": "string (required, min 8 chars)",
  "first_name": "string (required)",
  "last_name": "string (optional)"
}
```

## Response (201 Created)

```json
{
  "data": {
    "id": "uuid",
    "email": "string",
    "first_name": "string",
    "last_name": "string | null",
    "created_at": "ISO 8601 datetime"
  }
}
```

## Errors

| Status | Condition | Response |
|--------|-----------|----------|
| 400 | Invalid input | `{"detail": "Email is required"}` |
| 409 | Email exists | `{"detail": "Email already registered"}` |
| 422 | Validation | `{"detail": [{"loc": ["body", "email"], "msg": "Invalid email", "type": "value_error"}]}` |
| 500 | Server error | `{"detail": "Internal server error"}` |

## Notes
- Password is never returned in responses
- Email is case-insensitive (stored lowercase)
```

### 2. Storage

Save contracts to:
```
docs/api-contracts/
├── auth/
│   ├── login.md
│   └── register.md
├── users/
│   ├── list.md
│   ├── create.md
│   └── update.md
└── [feature]/
    └── [endpoint].md
```

### 3. Generate from Design

If a `/appbuilder-one:requirement-design` output exists, extract API
endpoints from the design and generate contract skeletons automatically.

Ask user to fill in details (exact field names, error cases).

### 4. Verify Implementation

`/appbuilder-one:api-contract verify` scans:
- Backend route handlers — do they match contract paths and methods?
- Request validation — does it check all required fields?
- Response format — does it match the contract schema?
- Error handling — are all documented error codes handled?
- Frontend API calls — do they send the right format and handle all errors?

Report mismatches:
```markdown
## Contract Verification: users/create

- [PASS] Endpoint path matches: POST /api/v1/users
- [FAIL] Request field mismatch: contract says "first_name", code uses "firstName"
- [PASS] Response format matches
- [FAIL] Error 409 not handled in frontend
- [WARN] Error 422 handler doesn't parse array format
```

### 5. Shared Types (TypeScript)

If both frontend and backend use TypeScript, generate shared types from
contracts:

```typescript
// types/api/users.ts (generated from contract)
export interface CreateUserRequest {
  email: string
  password: string
  first_name: string
  last_name?: string
}

export interface UserResponse {
  id: string
  email: string
  first_name: string
  last_name: string | null
  created_at: string
}
```

## Error Response Standard

All APIs must follow this error format:

```typescript
// String error
{ "detail": "Human-readable error message" }

// Validation errors (array)
{ "detail": [{ "loc": ["body", "field"], "msg": "Error message", "type": "error_type" }] }
```

Frontend must handle BOTH formats. See coding standards for the
`extractApiError()` utility pattern.

## Collaborative Protocol

- Create contract before implementation
- Both frontend and backend devs review the contract
- Changes to contracts require updating both sides
- Run verify after implementation to catch mismatches
