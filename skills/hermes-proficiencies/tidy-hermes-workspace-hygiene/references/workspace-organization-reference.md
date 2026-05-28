# Workspace Organization (Source Reference)

> **Source:** <private source path>/workspace/workspace-organization.md  
> **Status:** Reference copy for Hermes workspace-hygiene skill

## Objective

Any file created in this workspace can be found by a human or AI in under 30 seconds by drilling into logical categories — without scanning flat lists or relying on memory.

## Core Philosophy

Everything has a place. No clutter, no mess. The structure follows a logic that eliminates decision fatigue.

## Three-Tier Structure

```
workspace/
├── memory/     ← what happened    (state, logs, daily records, task tracking)
├── docs/       ← what we know     (research, projects, content, drafts, security)
└── ops/        ← how we work      (playbooks, SOPs, agenda, operational docs)
```

**When in doubt:** Is it a record of events? → `memory/`. Is it knowledge or research? → `docs/`. Is it process, protocol, or operations? → `ops/`.

## Key Rules

- Every new file is in the correct tier at creation.
- No folder has >15 files without subcategories.
- Lowercase, hyphens naming convention.
- No dates in filenames unless it's a log or archive.
- No `v2`, `final`, `improved`, `new` suffixes (use git history).

## Additional Categories

- `workbenches/` — Local tooling scaffolds and dev sandboxes only (not for final outputs)
- `scripts/` — Reusable utility scripts
- `tmp/` — Strictly disposable staging (gitignored)
- `logs/archive/` — Historical logs worth keeping

**Durable Local Code Rule:** Source checkouts, builds, symlinks, and LaunchAgents that must survive reboot must never live in `/tmp` or `/private/tmp`.
