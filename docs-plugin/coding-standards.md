# Coding Standards

## General

- All code must include doc comments on public APIs
- Every module must have a corresponding architecture decision record in `docs/architecture/`
- Business logic values must be data-driven (config/env), never hardcoded
- All public methods must be unit-testable (dependency injection over singletons)
- Commits must reference the relevant design document or task ID

## Frontend

### Stack (mandatory)
- **React** with TypeScript (strict mode)
- **Tailwind CSS** for all styling — no custom CSS files
- **shadcn/ui** as the component library — use before creating custom components
- **Lucide React** for ALL icons — **NEVER use raw SVGs, SVG files, or other icon libraries**

### Rules
- Components must be small and focused (single responsibility)
- Business logic must not live in components — extract to services/hooks
- All user-facing text must be extractable for i18n (no hardcoded strings in templates)
- Forms must have validation on both client and server
- All components must be typed with TypeScript (no `any`)
- Loading states required for all async operations
- Error states with user-friendly messages
- Responsive by default (mobile-first with Tailwind breakpoints)
- Use `context7` MCP to verify component APIs before using them

### Icons
```tsx
// ALWAYS — use Lucide React
import { Search, Plus, Settings } from 'lucide-react'

// NEVER — no SVGs, no other libraries
import { FaSearch } from 'react-icons/fa'  // FORBIDDEN
<svg>...</svg>                              // FORBIDDEN
import Icon from './icon.svg'               // FORBIDDEN
```

## Backend

- API endpoints must validate all input at the boundary
- Database queries must use parameterized queries (no string concatenation)
- Sensitive data must never appear in logs
- All endpoints must have authentication and authorization checks
- Error responses must not leak internal details

## Database

- All schema changes must go through migrations (never manual DDL)
- Tables must have created_at and updated_at timestamps
- Foreign keys must have explicit ON DELETE behavior
- Indexes must be added for frequently queried columns

## Testing

- **Verification-driven development**: Write tests first when adding business logic.
  For UI changes, verify with screenshots. Compare expected output to actual output
  before marking work complete. Every implementation should have a way to prove it works.

## Design Documents

- All design docs use Markdown
- Each module has a dedicated document in `design/product/`
- Documents must include these 8 required sections:
  1. **Overview** — one-paragraph summary
  2. **User Story** — who benefits and how
  3. **Detailed Design** — unambiguous rules and workflows
  4. **Data Model** — entities, fields, relationships
  5. **API Design** — endpoints, request/response schemas
  6. **Edge Cases** — unusual situations handled
  7. **Configuration** — configurable values identified
  8. **Acceptance Criteria** — testable success conditions
