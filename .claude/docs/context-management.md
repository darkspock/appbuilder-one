# Context Management

Context is the most critical resource in a Claude Code session. Manage it actively.

## File-Backed State (Primary Strategy)

**The file is the memory, not the conversation.** Conversations are ephemeral and
will be compacted or lost. Files on disk persist across compactions and session crashes.

### Session State File

Maintain `production/session-state/active.md` as a living checkpoint. Update it
after each significant milestone:

- Design section approved and written to file
- Architecture decision made
- Implementation milestone reached
- Test results obtained

### Incremental File Writing

When creating multi-section documents:

1. Create the file immediately with a skeleton (all section headers, empty bodies)
2. Discuss and draft one section at a time in conversation
3. Write each section to the file as soon as it's approved
4. Update the session state file after each section

## Proactive Compaction

- **Compact proactively** at ~60-70% context usage
- **Use `/clear`** between unrelated tasks
- **Natural compaction points:** after writing a section to file, after committing,
  after completing a task

## Subagent Delegation

Use subagents for research and exploration to keep the main session clean.

- **Use subagents** when investigating across multiple files or doing research
- **Use direct reads** when you know exactly which 1-2 files to check

## Recovery After Session Crash

1. Read `production/session-state/active.md` for context
2. Read the partially-completed file(s) listed in the state
3. Continue from the next incomplete section or task
