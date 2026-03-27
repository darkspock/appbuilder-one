# Design: [Feature Name]

*Created: [Date]*
*Status: Draft | Approved*
*Parent Epic: [link]*
*Architecture: [Standard / DDD]*

---

## Overview

[One paragraph: what this feature does and how it fits the epic]

---

## Data Model Changes

### New Entities

#### [Entity Name]

| Field | Type | Constraints | Description |
|-------|------|------------|-------------|

### Modified Entities

[Changes to existing tables/models]

### Migrations

[List of migrations needed]

---

## API Design

### [Endpoint Name]

- **Method**: [GET/POST/PUT/DELETE]
- **Path**: `/api/v1/...`
- **Auth**: [Required / Public]
- **Request:**
```json
{}
```
- **Response (200):**
```json
{}
```
- **Errors:**

| Status | Condition | Response |
|--------|-----------|----------|

---

## Backend Design

### For Standard Architecture:
- **Route/Controller**: [file path]
- **Service**: [business logic location]
- **Model**: [data model]

### For DDD Architecture:
- **Bounded Context**: [which BC]
- **Domain**: [entities, value objects, events]
- **Application**: [commands, queries]
- **Infrastructure**: [repositories]
- **Presentation**: [controllers, schemas]

---

## Frontend Design

- **Components**: [list of new/modified components]
- **State**: [state management approach]
- **API Integration**: [which endpoints, contract-first]
- **Error Handling**: [how errors are displayed]
- **Loading States**: [loading patterns]

---

## Test Strategy

- **Unit Tests**: [what to test]
- **Integration Tests**: [what to test]
- **E2E Tests**: [critical paths]

---

## Open Questions

| Question | Owner | Resolution |
|----------|-------|-----------|
