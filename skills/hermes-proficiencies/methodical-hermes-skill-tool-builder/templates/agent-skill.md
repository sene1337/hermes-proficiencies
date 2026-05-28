---
name: <skill-name>
description: Use when <specific trigger>. <runtime behavior/capability this installs>.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [<tags>]
    related_skills: [<related-skills>]
---

# <Skill Title>

## Overview

What behavior this skill installs and why it exists.

## When to Use

- Trigger conditions
- Counter-triggers / when not to use
- Related skills to use first/instead

## Runtime Contract

Invocation, action model, risk class, stop/ask/escalate rules, outputs, verification.

## Operating Procedure

Concrete steps Hermes should take when the skill is loaded.

## Progressive Disclosure

- `references/...` — when to load and why
- `templates/...` — when to use and expected output
- `scripts/...` — when to run and what it does
- `assets/...` — when needed

## Eval Cases

Minimal should-trigger / should-not-trigger / success / missing-context / dangerous-action cases.

## Common Pitfalls

- **Pitfall:** What goes wrong
  **Fix:** What to do instead

## Verification Checklist

- [ ] Checklist proving the skill is ready

## Change History
