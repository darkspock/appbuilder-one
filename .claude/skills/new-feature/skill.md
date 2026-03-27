# New Feature

Day-to-day skill for adding features to an existing app. Lighter than a full
module design — focused on getting from idea to implementation quickly.

## Usage

`/new-feature [description]` — e.g., `/new-feature add PDF export to invoices`

## Workflow

### 1. Understand the Feature

Ask (one at a time):
- What should the feature do? (if not clear from description)
- Which module does it belong to?
- Who uses it? (which roles)
- Is there an existing design doc to update?

### 2. Impact Analysis

- Read the relevant module GDD
- Read related module GDDs that might be affected
- Identify: new endpoints, new DB fields, new UI components, new tests needed

Present impact summary:
> **Feature: [name]**
> - Module: [name]
> - New endpoints: [list or none]
> - DB changes: [list or none]
> - UI changes: [list or none]
> - Tests needed: [list]
> - Estimated effort: [S/M/L]

### 3. Design (lightweight)

For small features (S): draft the changes in conversation, get approval, implement.
For medium features (M): create a mini-spec with rules, edge cases, acceptance criteria.
For large features (L): redirect to `/design-module` for full GDD treatment.

### 4. Implementation

- Write the code (with user approval at each step)
- Write tests
- Update the module GDD if design changed
- Update the modules index if scope changed

### 5. Verify

- Run tests
- Show the result (screenshot for UI, curl for API)
- Mark complete

## Collaborative Protocol

- Confirm understanding before coding
- Show impact analysis before implementing
- Test before marking done
