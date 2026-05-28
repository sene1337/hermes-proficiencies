# File Routing SOP (Source Reference)

> **Source:** <private source path>/workspace/sops/file-routing.md  
> **Status:** Reference copy for Hermes workspace-hygiene skill

## Core Rule

**Route every new file to the correct location at time of creation** — zero misplaced files, zero "I'll file it later."

## Three-Tier Decision

1. **memory/** — Events, logs, daily records, task state
2. **docs/** — Knowledge, research, projects, content
3. **ops/** — Process, protocol, operations, schedules

## Key Routing Principles

- File immediately in the same step it is created.
- Use git history instead of creating `-v2`, `-final`, `-improved` versions.
- Lowercase + hyphens naming.
- New standalone files should include an Origin block and Changelog.
- Subagent output must specify output path in the task description.
- System temp (`/tmp`, `/private/tmp`) is scratch only — never for durable work.

## Common Pitfalls Documented

- "I'll file it later"
- Using `/tmp` as a junk drawer
- Creating parallel version files instead of using git
- Leaving drafts in the wrong place
- Workbench sprawl (putting final outputs in `workbenches/`)

## Origin Story Requirement

Every new standalone file gets a one-line blockquote at the top stating when it was created, who made it, and why.
