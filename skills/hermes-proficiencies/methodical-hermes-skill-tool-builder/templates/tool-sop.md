---
name: <tool-or-capability-name>
description: Use when <trigger involving this tool/capability>. <what capability this unlocks and when it beats alternatives>.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [tool-sop, <tool-name>]
    related_skills: [<related-skills>]
---

# <Tool Name> Tool SOP

## Quick Ref

- Commands, endpoints, paths, env vars, tool calls, or API shapes
- Keep this usable in 10 seconds

## When to Use This

If/then decision tree covering:

- What this tool gives Hermes
- When it beats alternatives
- When not to use it
- Expected outputs and failure signals

## Runtime Contract

Allowed actions, forbidden actions, risk class, approval thresholds, stop/ask/escalate rules.

## Usage Patterns

### Pattern name

Exact steps, commands, tool calls, or request examples.

## Verification / Health Checks

How to confirm the tool call, command, or workflow worked.

## Gotchas & Lessons

- **What went wrong:** What to do instead.
- Reference real incidents or failure modes when possible.

## Support Files

- `references/...` for detailed docs or API notes
- `templates/...` for request/response bodies or config starters
- `scripts/...` for deterministic workflows

## Change History
