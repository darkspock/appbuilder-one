# Epic Writer

Create or update an epic (PRD) with full requirements specification.
Guides the user through writing a complete epic following the hierarchy
of technical impact: Foundation > Behavior > Aesthetics.

**Modes**: Solo (light), Team (full), Enterprise (full + compliance)

## Usage

`/epic [name]` — Create new epic
`/epic [path]` — Resume existing epic

Example: `/epic user-authentication`

## The Hierarchy of Technical Impact

| Level | What | Cost of Error |
|-------|------|---------------|
| **1. Foundation** | Entities, business logic, integration contracts | Critical |
| **2. Behavior** | Flows, states, edge cases | Medium |
| **3. Aesthetics** | Colors, spacing, copywriting | Low |

**Foundation must be defined 100% before coding starts.**
Behavior should be defined clearly. Aesthetics can be iterative.

## Workflow

### 1. Create Epic Folder

```
docs/working_docs/epics/[epic-name]/
├── requirements.md
└── attachments/
```

### 2. Guide Requirements Writing (ONE section at a time)

#### Section 1: Business Context
- Objective and value proposition
- Target users
- Business impact (measurable)
- Discovery reference (if applicable)

#### Section 2: Scope
- In-scope (explicit list)
- Out-of-scope (explicit list)
- Dependencies and prerequisites
- Assumptions
- Constraints
- Timeline

#### Section 3: Entities (CRITICAL — Level 1)
For each entity:
- **Properties** (business concepts, not technical)
- **Validations** (detailed — common source of bugs and data corruption)
- **Statuses** (lifecycle)
- **Status change rules** (transitions + events raised)

#### Section 4: Business Rules (CRITICAL — Level 1)
- Hard rules (must always be true)
- Compliance triggers
- Integration contracts (if external systems)

#### Section 5: User Flows (Level 2)
- Primary flow (step by step)
- Alternative flows
- Error flows
- Edge cases

#### Section 6: Non-Functional (Team/Enterprise)
- Performance expectations
- Scalability
- Observability/logging
- Accessibility
- Localization
- Feature flags

#### Section 7: Acceptance Criteria
- Testable conditions for each requirement
- Performance criteria
- Security criteria

### 3. Validate

After writing, suggest running `/requirement-validate` on the epic.

### 4. Next Steps

- If epic is large: `/requirement-slicing` to slice into features
- If epic is small: `/requirement-design` to create technical design
- If team mode: assign for TL review

## Collaborative Protocol

- One section at a time
- User provides business knowledge, AI structures it
- Flag ambiguities and missing information
- Never invent business rules — ask
- Write each section to file after approval
