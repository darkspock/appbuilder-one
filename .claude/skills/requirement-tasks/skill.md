# Requirement Tasks

Generate implementation tasks from an approved design document.
Tasks are ordered by architecture pattern and dependency.

**Modes**: All (depth varies)

## Usage

`/requirement-tasks [path-to-feature-folder]`

Example: `/requirement-tasks docs/working_docs/features/user-auth`

## Workflow

### 1. Read Context

- Feature `requirements.md`
- Feature `design.md` (must exist — run `/requirement-design` first)
- `.claude/docs/architecture/backend-architecture.md`
- `.claude/docs/technical-preferences.md`

### 2. Generate Tasks

Order depends on architecture:

#### For DDD Architecture:
1. Domain entities and value objects
2. Domain services
3. Application services (commands/queries)
4. Infrastructure (repositories)
5. API/Controllers
6. Frontend components
7. Tests

#### For MVC/Standard Architecture:
1. Database migrations
2. Models
3. Controllers/Routes
4. Services/Business logic
5. Frontend components
6. Tests

#### For Frontend-only changes:
1. Types/interfaces
2. API client functions
3. Hooks/state management
4. Components
5. Pages
6. Tests

### 3. Task Format

```markdown
# Tasks: [Feature Name]

## Status Legend
- [ ] Pending
- [~] In Progress
- [!] Blocked
- [?] In Review
- [x] Done

## Tasks

### Phase 1: Foundation

- [ ] **TASK-001**: [Description]
  - Acceptance: [What proves this is done]
  - Tests: [What to test]
  - Files: [Files to create/modify]

- [ ] **TASK-002**: [Description]
  - Acceptance: [criteria]
  - Tests: [what to test]
  - Blocked by: TASK-001
```

### 4. Task Completion Rules

A task is Done when:
- Code is committed
- Acceptance criteria met
- Tests pass
- Documentation updated if needed

### 5. Output

Write `tasks.md` to the feature folder.
Developer should review all tasks before starting.

## Collaborative Protocol

- Present tasks for review
- Developer can reorder or modify
- Tests must be included
