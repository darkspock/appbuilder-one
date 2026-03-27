---
name: code-review
description: Review code for quality, security, architecture compliance, and best practices. Checks against project coding standards.
---

# Code Review

Review code for quality, security, and architecture compliance.

## Usage

`/appbuilder-one:code-review` — Review uncommitted changes
`/appbuilder-one:code-review [file-or-dir]` — Review specific files
`/appbuilder-one:code-review --pr [number]` — Review a GitHub PR

## What It Checks

### Always (All modes)
- [ ] Code matches design document (if exists)
- [ ] No hardcoded secrets or credentials
- [ ] Error handling is appropriate
- [ ] No `console.log` left in production code
- [ ] TypeScript: no `any` types
- [ ] SQL: parameterized queries (no concatenation)

### Frontend (if applicable)
- [ ] Uses shadcn/ui components (not custom when existing component works)
- [ ] Icons from Lucide React only (no SVGs)
- [ ] Tailwind classes only (no custom CSS)
- [ ] Loading states for async operations
- [ ] Error states with user messages
- [ ] API errors extracted and displayed (not generic messages)
- [ ] Responsive design (mobile-first)

### Backend (if applicable)
- [ ] Input validation at API boundary
- [ ] Auth/authorization on all endpoints
- [ ] Error responses don't leak internals
- [ ] Sensitive data not in logs
- [ ] Database migrations for schema changes

### Architecture (if DDD)
- [ ] No business logic in controllers
- [ ] No direct database access outside repositories
- [ ] Commands for writes, queries for reads (CQRS)
- [ ] Domain entities have no framework dependencies

### Tests
- [ ] Tests exist for new business logic
- [ ] Tests are meaningful (not just coverage)
- [ ] Edge cases tested

## Output

```markdown
# Code Review: [scope]

## Summary
- Issues: [N critical] [N warning] [N suggestion]
- Files reviewed: [N]

## Issues

### [CRITICAL] SQL injection risk
- **File**: src/users/controller.ts:45
- **Issue**: String concatenation in query
- **Fix**: Use parameterized query

### [WARNING] Missing error handling
- **File**: src/components/UserForm.tsx:23
- **Issue**: API call without try/catch
- **Fix**: Add error handling with extractApiError()

### [SUGGESTION] Could use shadcn/ui Dialog
- **File**: src/components/ConfirmModal.tsx
- **Issue**: Custom modal when shadcn/ui Dialog exists
- **Fix**: Replace with Dialog component
```

## Collaborative Protocol

- Report findings, don't auto-fix
- Prioritize: critical first, suggestions last
- Offer to fix issues one by one after review
