# Requirement Design

Generate technical design for a validated feature. Checks current codebase,
architecture docs, and requirements to produce a design document.

**Modes**: Solo (light), Team (full), Enterprise (full + review gate)

## Usage

`/requirement-design [path-to-feature-folder]`

Example: `/requirement-design docs/working_docs/features/user-auth`

## Workflow

### 1. Gather Context

Read:
- Feature `requirements.md`
- Feature `validation.md`
- `.claude/docs/architecture/backend-architecture.md` (if exists)
- `.claude/docs/architecture/frontend-standards.md` (if exists)
- `.claude/docs/technical-preferences.md`
- Current codebase structure
- Related existing code

### 2. Generate Design

Create `design.md` with:

#### For Standard Architecture:
- Components to create/modify
- Data model changes (migrations, models)
- API contracts (endpoints, request/response)
- Frontend components needed
- Integration points
- Test strategy

#### For DDD Architecture:
- Bounded context placement
- Domain entities and value objects
- Commands and queries (CQRS)
- Domain events
- Repository interfaces (ports)
- Infrastructure implementations (adapters)
- HTTP controllers and routers
- Request/Response schemas
- Test strategy

#### For Frontend (Guided mode):
- Component hierarchy
- State management approach
- API integration (contract-first)
- Error handling
- Loading states
- Responsive requirements

### 3. Review Gate (Team/Enterprise)

Design must be approved by TL/senior before task generation.

Present design summary and ask for approval.

### 4. Output

Write `design.md` to the feature folder.
Ask approval before writing.

## Collaborative Protocol

- Present design for review before writing
- Flag architectural concerns
- User/TL approves before proceeding to tasks
