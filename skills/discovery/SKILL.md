---
name: discovery
description: Product Discovery process — validate whether a feature or product is worth building before writing code.
---

# Product Discovery

Validate whether a feature or product is worth building before writing
requirements or code. Answers: "Is this worth building?"

**Modes**: Team, Enterprise (optional in Solo, skip in Learning)

## When to Run

- New product or major feature
- Significant investment (> 2 weeks effort)
- High uncertainty about user needs
- Entering new market or user segment

## When to Skip

- Bug fixes or technical debt
- Regulatory compliance (must-do)
- Direct customer request with clear specs
- Small enhancements (< 3 days effort)

## Workflow

### Phase 1: Frame the Opportunity

Ask ONE question at a time to build the opportunity brief:

1. **What problem are you trying to solve?**
2. **Who has this problem?** (target users)
3. **How is it solved today?** (current solutions, workarounds)
4. **What's the business value?** (revenue, efficiency, retention)
5. **What assumptions are we making?** (list 3-5 key assumptions)

**Enterprise mode adds:**
6. **Personal data involved?** → GDPR implications
7. **Automated decisions?** → EU AI Act classification
8. **Sector regulations?** → Financial, health, minors

Save to `docs/working_docs/discovery/[opportunity-name]/opportunity_brief.md`

### Phase 2: Research & Learn

Guide the user through research methods:

| Method | Best For | Effort |
|--------|----------|--------|
| User Interviews | Deep understanding | High |
| Surveys | Quantitative validation | Medium |
| Analytics Review | Current behavior | Low |
| Support Analysis | Pain points | Low |
| Competitor Analysis | Market gaps | Medium |

AI can help analyze research inputs:
- Synthesize interview notes
- Identify patterns in survey data
- Compare competitors

Save to `docs/working_docs/discovery/[opportunity-name]/research_findings.md`

### Phase 3: Prototype & Validate

Guide prototype creation:

| Fidelity | When | Tools |
|----------|------|-------|
| Sketch | Exploring concepts | Paper, Excalidraw |
| Lo-Fi | Testing flow | Figma, Balsamiq |
| Hi-Fi | Final validation | Figma, coded prototype |
| Code Prototype | Technical feasibility | V0, Lovable, Bolt |

**Important**: Before prototyping, document non-negotiable business rules.
AI prototyping tools invent rules that may be wrong.

Save to `docs/working_docs/discovery/[opportunity-name]/prototype_validation.md`

### Phase 4: Go/No-Go Decision

Score the opportunity:

| Criteria | Weight |
|----------|--------|
| Problem validated | 25% |
| Solution validated | 25% |
| Business value clear | 20% |
| Feasible to build | 15% |
| Acceptable risk | 15% |

**Thresholds:**
- **> 4.0**: Strong GO → proceed to Development
- **3.0-4.0**: Conditional GO → proceed with mitigations
- **2.0-3.0**: More Discovery needed
- **< 2.0**: NO-GO → archive learnings

Save to `docs/working_docs/discovery/[opportunity-name]/discovery_decision.md`

### Phase 5: Handoff to Development

If GO:
1. Create epic folder in `docs/working_docs/epics/[epic-name]/`
2. Write requirements using Discovery outputs
3. Proceed to Development Workflow

## Archive No-Go Decisions

Save to `docs/archived_discovery/[YYYY-MM]-[name]/` with a `lessons_learned.md`.
Future discoveries can reference past learnings.

## Collaborative Protocol

- One question at a time
- User makes all judgment calls
- AI assists analysis, user owns decisions
- Ask before writing any file
