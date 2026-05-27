# Skill-dev Source Layout Regressions

Use this reference when auditing or cleaning Hermes skill-development source repos after duplicate placement, wrong repo routing, or redundant wrapper folders.

## Correct private source repo model

Private skill-development repos are source libraries. Their internal folder shape should reflect the repo's purpose, not blindly mirror installed runtime layout.

### Hermes proficiencies source repo

Canonical source repo:

```text
<PUBLISH_WORKSPACE>/
  <skill-name>/
    SKILL.md
    references/
    templates/
    scripts/
    assets/
```

Do not nest proficiencies under redundant wrappers:

```text
<PUBLISH_WORKSPACE>/skills/software-development/<skill-name>/  # wrong unless intentionally mirroring runtime packaging
```

### Soulbound/tool skills source repo

Canonical source repo:

```text
<PRIVATE_TOOL_SKILLS_WORKSPACE>/
  <domain>/
    <tool-or-capability-skill>/
      SKILL.md
      references/
      templates/
      scripts/
      assets/
```

Soulbound/tool skills may keep a domain folder like `devops/` because the repo is a tool-skill library and domain grouping is part of the source taxonomy.

### Installed runtime layout

Runtime remains category-based under Hermes:

```text
~/.hermes/skills/<category>/<skill-name>/
~/.hermes/skills/<skill-name>/  # flat install is also supported
```

Examples:

```text
~/.hermes/skills/devops/1password-cli/
~/.hermes/skills/productivity/google-workspace/
```

Hermes supports these category folders natively, but it does not make `software-development` the required category. Category choice should be deliberate and based on the skill's operating role.

Runtime layout is not automatically the right source-repo layout.

## Regression pattern from 2026-05-27

A Hermes proficiency (`tidy-hermes-workspace-hygiene`) ended up in two source repos:

```text
<PUBLISH_WORKSPACE>/skills/software-development/tidy-hermes-workspace-hygiene/  # intended repo, wrong wrapper layout
<PRIVATE_TOOL_SKILLS_WORKSPACE>/software-development/tidy-hermes-workspace-hygiene/                     # wrong repo and wrong class
```

The first review focused on runtime/source drift and content score, but missed the real structural regression: duplicate source placement and wrong artifact-class routing.

Corrective actions taken:

1. Removed the duplicate proficiency from `soulbound-skills`.
2. Flattened `hermes-proficiencies` so proficiencies live at repo root.
3. Preserved runtime installs under the appropriate Hermes runtime category.
4. Updated `tidy-hermes-workspace-hygiene` and `methodical-hermes-skill-tool-builder` to check for duplicate placement and redundant wrappers.

## Audit checklist

Before scoring or rewriting skill prose during a skill-dev regression audit:

- [ ] Identify the artifact class: Hermes proficiency, soulbound/tool skill, human playbook/SOP, or runtime-only experiment.
- [ ] Search sibling source repos for the same skill directory name.
- [ ] Confirm the skill exists in exactly one canonical source repo.
- [ ] Confirm source layout follows repo purpose, not runtime layout by habit.
- [ ] Confirm installed runtime copies are treated as runtime, not source of truth.
- [ ] Check git status in each affected source repo before moving/deleting.
- [ ] Use `git mv` for source layout migrations so history is preserved.
- [ ] Ask for explicit scope before deleting or removing tracked duplicate directories.
- [ ] After cleanup, verify no duplicate path remains and source/runtime copies are reconciled where applicable.

## Rule of thumb

If a repo name already describes the library type, avoid repeating that classification as wrapper folders inside the repo. Keep source repos easy to scan and reserve runtime/category nesting for the installed Hermes runtime tree.
