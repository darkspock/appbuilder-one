---
name: status
description: Show project status dashboard. Modules designed, features in progress, tests passing, last deploy, open issues.
---

# Project Status

Quick overview of where the project stands.

## Usage

`/appbuilder-one:status` — Full status dashboard
`/appbuilder-one:status modules` — Module design progress only
`/appbuilder-one:status tests` — Test results only
`/appbuilder-one:status deploy` — Deployment status only

## Workflow

### 1. Gather Data

Read from multiple sources:

**Design progress:**
- Read `design/product/modules-index.md` — module design status
- Count GDDs: total, designed, approved, implemented
- Read `docs/working_docs/epics/` — active epics
- Read `docs/working_docs/features/` — features in progress

**Code status:**
- `git status` — uncommitted changes
- `git log --oneline -5` — recent commits
- Count source files by type

**Tests:**
- Run test suite (`npm test` / `pytest` / etc.)
- Extract pass/fail counts
- Show coverage if available

**Dependencies:**
- `npm audit` / `pip audit` — vulnerability count
- Check for outdated packages

**Deploy:**
- Last deploy date (from git tags or hosting CLI)
- Current environment status
- Check if local is ahead of deployed

**GitHub:**
- `gh pr list` — open PRs
- `gh issue list` — open issues
- `gh run list -L 3` — recent CI runs

### 2. Display Dashboard

```markdown
# Project Status — [date]

## Design
- Modules: [5/12 designed] [3/12 approved] [1/12 implemented]
- Active epics: [2]
- Features in progress: [3]

## Code
- Recent: [last commit message] ([time ago])
- Uncommitted changes: [yes/no]
- Source files: [N] files across [N] directories

## Tests
- Pass: [N] | Fail: [N] | Skip: [N]
- Coverage: [X%]
- Last run: [time]

## Security
- Vulnerabilities: [N critical] [N high] [N moderate]

## Deploy
- Last deploy: [date] to [environment]
- Local vs deployed: [N commits ahead]
- Status: [healthy / failing / unknown]

## GitHub
- Open PRs: [N]
- Open issues: [N]
- Last CI: [pass/fail] ([time ago])

## Next Actions
- [Suggested next step based on status]
```

### 3. Suggest Next Actions

Based on status, recommend:

| Situation | Suggestion |
|-----------|-----------|
| No modules designed | Run `/appbuilder-one:map-modules` |
| Modules designed but no code | Run `/appbuilder-one:init` or start implementing |
| Tests failing | Fix failing tests before continuing |
| Vulnerabilities found | Run `/appbuilder-one:check-security` |
| Ahead of deploy | Run `/appbuilder-one:deploy staging` |
| No recent commits | Check if work is in progress or stalled |
| Open PRs aging | Review and merge or close |

## Collaborative Protocol

- Read-only operation, never modifies files
- Quick to run, no heavy analysis
- Show only what's relevant (skip empty sections)
