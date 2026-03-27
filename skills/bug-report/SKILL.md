---
name: bug-report
description: Document and diagnose a bug. Creates a structured report, investigates root cause, and suggests a fix.
---

# Bug Report

Document, diagnose, and fix bugs with a structured approach.

## Usage

`/appbuilder-one:bug-report [description]`

Example: `/appbuilder-one:bug-report users can't login after password reset`

## Workflow

### 1. Gather Information

Ask ONE question at a time:
- What's happening? (actual behavior)
- What should happen? (expected behavior)
- Steps to reproduce?
- When did it start? (recent change?)
- Any error messages?

### 2. Investigate

- Search codebase for related code
- Check recent git commits (`git log --oneline -20`)
- Check error logs if available
- Identify the root cause

### 3. Create Bug Report

Save to `docs/working_docs/hotfixes/[bug-name]/requirements.md`:

```markdown
# Bug: [Title]

**Reported**: [date]
**Severity**: [Critical / High / Medium / Low]
**Status**: [Open / Investigating / Fix Ready / Resolved]

## Description
[What's broken]

## Steps to Reproduce
1. [Step 1]
2. [Step 2]
3. [Expected: X, Actual: Y]

## Root Cause
[Why it's happening]

## Fix
[What to change]

## Files Affected
- [file:line]

## Testing
- [ ] [How to verify the fix]
```

### 4. Fix

- Implement the fix
- Write a test that would have caught the bug
- Verify the fix works

### 5. Severity Guide

| Severity | Criteria | Response Time |
|----------|----------|---------------|
| **Critical** | App down, data loss, security breach | Immediate |
| **High** | Major feature broken, workaround exists | Same day |
| **Medium** | Minor feature broken, edge case | This sprint |
| **Low** | Cosmetic, minor inconvenience | Backlog |
