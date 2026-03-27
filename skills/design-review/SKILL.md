---
name: design-review
description: Review a design document for completeness, consistency, implementability, and adherence to project standards.
---

# Design Review

Validate a design document before handing it to developers.

## Usage

`/appbuilder-one:design-review [path-to-doc]`

Example: `/appbuilder-one:design-review docs/working_docs/features/user-auth/design.md`

## What It Checks

### Completeness
- [ ] All required sections present and filled
- [ ] Data model has all fields, types, and constraints
- [ ] API endpoints have request/response schemas
- [ ] Error cases documented
- [ ] Edge cases identified
- [ ] Acceptance criteria are testable

### Consistency
- [ ] Field names match across data model, API, and frontend
- [ ] Status values consistent between design and API
- [ ] No contradictions between sections
- [ ] Matches parent epic requirements

### Implementability
- [ ] A developer could implement without asking questions
- [ ] No hand-waving ("handle gracefully", "make it work")
- [ ] Performance implications considered
- [ ] Migration path clear for existing data

### Architecture Compliance
- [ ] Follows project architecture (DDD or standard)
- [ ] No violations of coding standards
- [ ] Dependencies are appropriate
- [ ] API follows contract standards

### Cross-Reference
- [ ] Doesn't contradict other module designs
- [ ] Shared entities are consistent across modules
- [ ] API contracts match between frontend and backend

## Output

```markdown
# Design Review: [document]

## Verdict: [APPROVED / NEEDS REVISION / BLOCKED]

## Findings

### Must Fix
- [Issue 1 — why it matters]

### Should Fix
- [Issue 1 — improvement]

### Notes
- [Observation that doesn't block approval]
```

## Collaborative Protocol

- Read the full document before commenting
- Verdict must be clear: approved, needs revision, or blocked
- For "needs revision": list exactly what needs to change
- User decides whether to fix or proceed with known gaps
