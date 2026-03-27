# Requirement Validate

Validate an epic or feature's requirements for completeness and clarity.
Content-based validation, not template-based.

**Modes**: Solo (light), Team (full), Enterprise (full + compliance)

## Usage

`/requirement-validate [path-to-folder]`

Example: `/requirement-validate docs/working_docs/epics/user-auth`

## Workflow

### 1. Read Requirements

Read `requirements.md` from the specified folder.

### 2. Validate by Category

Ask clarifying questions ONE AT A TIME to fill gaps.
Write findings to `validation.md` in the same folder.

#### A. Business Alignment (All modes)

- [ ] Objective and value proposition explicit
- [ ] Target users specified
- [ ] Business impact measurable

#### B. Scope and Boundaries (All modes)

- [ ] In-scope items listed
- [ ] Out-of-scope items listed
- [ ] Dependencies listed
- [ ] Assumptions documented

#### C. Compliance (Enterprise mode only)

- [ ] GDPR requirements addressed
- [ ] Data protection requirements
- [ ] Security constraints stated
- [ ] Key risks with mitigations

#### D. Functional Coverage (All modes)

- [ ] Primary entities identified with properties
- [ ] CRUD operations addressed
- [ ] Statuses and transitions defined
- [ ] Normal use cases documented
- [ ] Edge cases documented
- [ ] Error scenarios documented

**Entity Definition Guide:**
For each new entity, document at minimum:
- Properties (business concepts, not technical)
- Validations (detailed — common source of bugs)
- Statuses (lifecycle)
- Status change rules (what happens on each transition)

#### E. Non-Functional (Team/Enterprise)

- [ ] Performance expectations
- [ ] Scalability requirements
- [ ] Observability/logging needs
- [ ] Accessibility requirements
- [ ] Localization requirements
- [ ] Feature flag requirements

### 3. Decision

| Decision | Action |
|----------|--------|
| **Approved** | Proceed to design/slicing |
| **Approved with Risks** | Proceed with documented risks |
| **Needs Revision** | Return for updates |
| **Blocked** | Escalate |

### 4. Output

Write `validation.md` with all findings and decision.

## Collaborative Protocol

- Ask clarifying questions one at a time
- Flag missing items, don't invent requirements
- User decides whether gaps are acceptable
