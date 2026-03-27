# Directory Structure

```text
/
├── CLAUDE.md                    # Master configuration
├── .claude/                     # Agent definitions, skills, hooks, rules, docs
│   ├── docs/
│   │   ├── project-mode.md      # Active mode (learning/solo/team/enterprise)
│   │   ├── technical-preferences.md
│   │   ├── architecture/        # Backend and frontend architecture rules
│   │   └── templates/           # Document templates
│   └── skills/                  # Slash command definitions
├── src/                         # Application source code
│   ├── frontend/                # Frontend code
│   ├── backend/                 # Backend code
│   ├── shared/                  # Shared types, utils
│   └── database/                # Migrations, seeds, models
├── design/                      # Product design documents
│   ├── product/                 # Product specs, PRDs, user stories
│   ├── wireframes/              # UI wireframes and mockups
│   └── user-flows/              # User flow diagrams
├── docs/                        # Technical and working documentation
│   ├── architecture/            # ADRs and architecture docs
│   ├── api/                     # API documentation
│   ├── working_docs/            # Active development documentation
│   │   ├── discovery/           # Product Discovery artifacts
│   │   ├── epics/               # Epic requirements and validation
│   │   ├── features/            # Feature design, tasks, validation
│   │   ├── hotfixes/            # Emergency fix documentation
│   │   └── cases/               # Investigation-only work
│   └── archived_discovery/      # Archived NO-GO discoveries (corporate memory)
├── tests/                       # Test suites
├── tools/                       # Build and pipeline tools
└── production/                  # Production management
    ├── sprints/                 # Sprint plans
    ├── milestones/              # Milestone definitions
    ├── session-state/           # Ephemeral session state (gitignored)
    └── session-logs/            # Session audit trail (gitignored)
```
