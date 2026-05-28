# thorough-hermes-skill-publishing

Hermes proficiency skill for thoroughly preparing and publishing other skills.

## What it does

Enforces operational discipline when turning working local behavior into clean, portable, shareable skills. Covers:

- Runtime validation before packaging
- Removing private data and machine-specific references
- Safe syncing from workspace to publishable repos
- Artifact hygiene checks
- Pre-publish quality gates

## Installation

Copy the entire `thorough-hermes-skill-publishing` folder into your Hermes skills directory:

```bash
~/.hermes/skills/software-development/thorough-hermes-skill-publishing/
```

Then restart Hermes so the skill is picked up.

## When it loads

Automatically loads when you are preparing a skill for distribution or public sharing.

## Related Skills

- `hermes-agent-skill-authoring` — Writing the actual skill content
- `tidy-hermes-workspace-hygiene` — General file and git discipline

## Origin

Adapted from the source Skill Publishing SOP with adjustments for Hermes' architecture and tooling.
