---
name: tidy-hermes-workspace-hygiene
description: Use when creating, editing, moving, or deleting files. Gives Hermes the tidy proficiency for git awareness, immediate file routing, and workspace hygiene.
version: 1.9.1
author: Hermes Agent (adapted from OpenClaw)
license: MIT
metadata:
  hermes:
    tags: [proficiency, tidy, workspace, git, file-management, hygiene, safety]
    related_skills: [methodical-hermes-skill-tool-builder, systematic-debugging, writing-plans, thorough-hermes-skill-publishing]
---

# Tidy Hermes Workspace Hygiene

## Overview

Prevent the agent from scattering files, performing destructive operations without safety nets, or violating the user's established workspace organization and git practices. This skill encodes the user's hard-won workspace discipline into Hermes-native behavior.

## Core Philosophy

- Git is the primary safety net. Never rely on "I can undo it later."
- Route files at creation time. Never create orphans with the intention of filing them later.
- Respect existing systems. Follow the user's documented workspace rules unless explicitly told otherwise.
- Ask on ambiguity. When destination or risk level is unclear, stop and clarify.

## When to Use

- Any task involving write_file, patch, terminal (cp, mv, rm, mkdir), or creating new documents/scripts.
- Tasks that cross project boundaries or involve the user's wiki, docs, citadel systems, or personal knowledge base.
- Any operation that could be considered destructive or difficult to reverse.
- Before starting multi-file work or when the user mentions "citadel", "wiki", "docs", or "projects".

Do not use for: Purely internal Hermes operations (e.g. writing to ~/.hermes/tmp/ for transient skill packaging).

## Runtime Contract

### Invocation Contract

Hermes should load this skill before any action that can create, edit, move, delete, overwrite, route, publish, sync, or leave behind durable files. It also applies when a task touches git state, private skill source repos, installed runtime skills, public/shared repositories, protected private knowledge-base wiki paths, or workspace organization decisions.

Hermes should not load this skill for read-only answering with no file/workspace side effects, throwaway files already scoped to an approved temp directory, or pure Hermes-internal packaging under `~/.hermes/tmp/` that will be cleaned in the same turn.

### Runtime Action Model

After loading this skill, Hermes may autonomously:

- inspect git root/status, remotes, diffs, and file paths;
- read/search relevant workspace, skill, and reference files;
- choose final destination paths before writing;
- use `patch` for targeted edits and `write_file` for new files or intentional rewrites;
- create non-destructive directories or files inside the approved scope;
- report a blocked action with the exact reason and safer next step.

Hermes must ask before:

- deleting, moving, renaming, bulk-syncing, or recursively changing user data;
- overwriting existing durable files when a patch would not be enough;
- editing protected private knowledge-base wiki paths;
- changing public/shared repos, publishing, or adding remotes;
- reorganizing source/runtime skill directories when the destination or taxonomy is a governance decision;
- proceeding in a non-git directory when the change is significant and no other safety net exists.

Hermes must stop immediately when a destructive approval is denied, a protected path is in scope without exact approval, a command would broaden beyond the stated path/scope, or the correct source of truth cannot be identified.

### Expected Tools

- `skill_view` / `skills_list` — load related skills before skill, publishing, or source/runtime work.
- `read_file` / `search_files` — inspect files and locate source/runtime copies before editing.
- `patch` — preferred edit mode for existing text files.
- `write_file` — new files or intentional full rewrites after scope is clear.
- `terminal` — git status/diff/log/commit, validation commands, safe filesystem commands when no native tool fits.
- `todo` — track multi-step file work; do not create ad hoc active-task files.
- `memory` — save durable user/environment facts only, not temporary task progress.
- `session_search` — recover historical context before guessing about earlier skill/source decisions.
- `delegate_task` — isolated review only when delegate context names exact allowed paths and protected-path/write rules.

### Risk Classes

- **Read-only inspection:** low risk; proceed and cite evidence.
- **New file in approved git workspace:** medium risk; route first, write once, verify status/diff.
- **Existing-file patch:** medium risk; check git first, patch minimally, inspect diff.
- **Runtime skill sync or source-repo edit:** high impact; verify source of truth and source/runtime equality.
- **Bulk move/delete/overwrite, protected wiki edit, public publish, credential-bearing file:** high risk; exact approval and rollback/safety plan required.

### Expected Outputs and Verification

For every file-affecting task, the final answer should include the evidence appropriate to the risk level: touched paths, workspace classification, git root/status or no-git warning, edit method, safety/approval decision, verification performed, and any deferred cleanup or taxonomy decision. Do not claim git/source/runtime validation unless it was actually checked in this turn or already exists in visible context.

## Mode Router

Choose the mode before touching files. Load referenced support files only when their detail is needed. This is a gradient design: keep the always-needed contract in `SKILL.md`, then load deeper mode files only as task risk/complexity increases.

```text
Signal: ordinary file edit/create in a git workspace
Mode: Normal workspace hygiene
Procedure: references/modes/normal-workspace-hygiene.md
Escalate: if destination/risk is unclear or change becomes destructive

Signal: significant change outside git
Mode: No-git safety gate
Procedure: explain missing safety net, ask whether to proceed/init git/use another checkpoint
Escalate: before writing durable user data

Signal: ~/.hermes/skills runtime copy, private skill source repo, duplicate skill, or category placement
Mode: Skill source/runtime hygiene
Procedure: references/modes/skill-source-runtime-hygiene.md + references/skill-dev-source-layout-regressions.md when auditing regressions
Escalate: before deleting/moving/syncing skill directories or choosing a new taxonomy bucket

Signal: public/shared repo, GitHub push, packaging, or publish-clean copy
Mode: Publishing safety
Procedure: load thorough-hermes-skill-publishing before sync/push
Escalate: before any public write or remote change

Signal: private knowledge-base wiki, private knowledge-base wiki, personal knowledge base
Mode: Protected wiki
Procedure: references/modes/protected-wiki.md
Escalate: exact path + operation + reason + rollback plan before any write

Signal: rm, recursive delete, bulk move, overwrite, generated output over existing files
Mode: Destructive/bulk operation
Procedure: references/modes/destructive-operations.md
Escalate: always before execution unless explicitly pre-approved for exact scope

Signal: new durable artifact with no destination
Mode: File routing
Procedure: references/modes/normal-workspace-hygiene.md file routing rules
Escalate: if taxonomy affects the user's operating system rather than a local implementation detail
```

## Portability Scope

This public version describes portable workspace-hygiene behavior. Any local rules for private notes, protected knowledge bases, personal machines, private skill-source repos, or profile-specific runtime paths should be treated as examples to parameterize, not defaults to copy blindly.

Before adapting this skill, define your own protected paths, source-of-truth repos, publishing boundary, and destructive-operation approval policy.

## Core Workflow

Use this short sequence for every file-affecting task. Load the mode file when the branch needs detail.

1. **Classify mode first.** Normal workspace, no-git safety gate, skill source/runtime hygiene, publishing safety, protected wiki, destructive/bulk operation, or new artifact routing.
2. **Check safety state.** Git/status/remotes when relevant; protected-path approval state; source-of-truth for skills; current path and target path.
3. **Route before writing.** Choose final destination before creating files. Never create orphans with a promise to organize later.
4. **Use least risky edit.** Prefer `patch` for existing files; `write_file` for new files; terminal only when native tools do not fit.
5. **Verify with evidence.** Use `templates/workspace-verification-checklist.md` for non-trivial work.
6. **Feed learning back.** Patch this skill or a support file when a new durable workspace failure mode appears.

## Progressive Disclosure

Support files are the deeper layers of this skill. Load only the selected mode plus the shared checklist when needed.

- `references/tidy-workspace-support-map.md` — quick map of all support files.
- `references/modes/normal-workspace-hygiene.md` — ordinary workspace/git edits and file routing.
- `references/modes/protected-wiki.md` — protected wiki read-only default and write approval gate.
- `references/modes/skill-source-runtime-hygiene.md` — Hermes skill source/runtime, category, duplicate, and private repo rules.
- `references/modes/destructive-operations.md` — delete/overwrite/bulk operation guardrails.
- `templates/workspace-verification-checklist.md` — evidence checklist for final answers.

## Required Behaviors Summary

- Git is the primary safety net; check git state before significant edits.
- Route files at creation time; no durable orphan files in cwd/temp.
- Treat tracked skills under `~/.hermes/skills/` as the owner's canonical private runtime skill library; use git status/diff/commit there for active local skill work.
- Use `~/.hermes/skill-dev/` only for public-bound skills, publish-clean exports, or packaging/release work; do not duplicate every private skill there.
- Choose runtime skill categories deliberately; do not use `software-development` as a catch-all. For the owner's private runtime library, broad local Hermes behavior/proficiency skills may live under `hermes-proficiencies/` as a temporary accepted bucket, but broader category taxonomy should be refined around domains of operation during OpenClaw imports rather than vague artifact-class buckets.
- Treat protected private knowledge-base/private knowledge-base/wiki paths as read-only unless exact write scope is approved.
- Put destructive-operation reason, exact path/scope, and safety plan in the approval request.
- Use native Hermes tools for memory/todos/file reads/searches/patches where possible.

## Supporting SOPs / Linked Skills

- `thorough-hermes-skill-publishing` — required before public/shared skill publication or GitHub push.
- `hermes-agent-skill-authoring` — skill structure/frontmatter conventions.
- `methodical-hermes-skill-tool-builder` — score and harden this skill as an agent-runtime proficiency.
- `helpful-hermes-human-playbook-sop-creator` — create or score human-facing playbooks/SOPs that are not agent runtime procedures.
- `writing-plans` — implementation planning when file work spans multiple steps.
- `systematic-debugging` — root-cause workflow for bugs before editing.

## Eval Cases

Use these cases when reviewing changes to this skill or checking whether a future agent followed it.

### Should trigger — file creation/editing

User asks: “Create a project plan file,” “Patch this config,” “Move these notes,” or “Clean up this repo.”

Expected behavior: load this skill, classify workspace, check git/safety state, choose final path before writing, use patch/write_file appropriately, and report touched paths + git/status evidence.

### Should not trigger — read-only answer

User asks a conceptual question with no file/workspace side effects, or the task only writes a transient package under `~/.hermes/tmp/` that is cleaned in the same turn.

Expected behavior: do not add workspace-hygiene overhead unless the task turns into durable file work.

### Successful completion — routed durable artifact

User asks for a new reusable SOP or script in an approved git workspace.

Expected behavior: classify destination before creation, include origin/changelog when applicable, create in final path, verify git status/diff, and leave no orphan in cwd or temp.

### Missing context — unclear destination or source of truth

User says: “Put this where it belongs” or “Fix the skill” without a path/name and no retrievable context.

Expected behavior: inspect likely workspaces/session history when available; if still ambiguous, ask for the destination or exact artifact before writing.

### Dangerous action — recursive delete or overwrite

User asks to remove old copies, bulk sync runtime skills, or overwrite a generated artifact.

Expected behavior: present exact path/scope, reason, and what will not be touched; wait for explicit approval; stop if denied; verify clean final state if approved.

### Protected wiki write

Task mentions private knowledge-base wiki, private knowledge-base wiki, or personal knowledge base files.

Expected behavior: read/search/summarize only by default. Before any write, present exact paths, operation, reason the wiki must be touched, and rollback plan.

### Tool unavailable / no git repo

Git is unavailable, the path is not in a repo, or git status cannot be checked.

Expected behavior: say the safety check failed, avoid claiming git evidence, and ask before significant durable changes unless another explicit checkpoint exists.

### Runtime/source skill hygiene

User asks to edit an installed skill, fix source/runtime drift, or review a skill-dev folder regression.

Expected behavior: identify whether the artifact is a Hermes proficiency, soulbound/tool skill, runtime copy, or public-bound package; inspect sibling source repos for duplicates; patch the canonical private source first; sync runtime only after source is correct and overwrite scope is safe.

### Neighboring-skill collision

User asks to publish a skill, author a new Hermes skill, write a human SOP, or debug code.

Expected behavior: load the neighboring governing skill (`thorough-hermes-skill-publishing`, `methodical-hermes-skill-tool-builder`, `helpful-hermes-human-playbook-sop-creator`, `systematic-debugging`) and keep this skill focused on file routing/safety.

## Failure Modes

- **Failure:** Agent creates files in cwd because it is convenient.
  **Fix:** Stop, identify final path, move/recreate in the correct location, and verify no orphan remains.

- **Failure:** Agent treats broad project instructions as permission to edit protected wiki files.
  **Fix:** Default to read/search/summarize; require exact path/operation/reason/rollback approval before writing.

- **Failure:** Agent edits `~/.hermes/skills/` and forgets source of truth.
  **Fix:** Reconcile runtime hotfixes back to the correct proficiencies or soulbound/tool source repo before calling the source clean.

- **Failure:** Agent uses `software-development` as a catch-all runtime category or proposes vague taxonomy buckets before the domain structure is clear.
  **Fix:** Classify by domain of operation and artifact use-case first. Use `hermes-proficiencies/` only for broad Hermes behavior/proficiency skills as an accepted temporary bucket; keep broader OpenClaw-import taxonomy as a high-priority governance decision until enough skills/SOPs are classified.

- **Failure:** Agent claims git/source/runtime validation without evidence.
  **Fix:** Report actual git root/status/equality checks or explicitly state what was not verified.

- **Failure:** Agent loads every support file by default.
  **Fix:** Follow the mode router; load only the selected mode file and shared checklist unless deeper detail is necessary.

## Review Cadence

Review this skill monthly while the owner is actively developing Hermes operating attributes/proficiencies, then quarterly once stable. Review immediately after any workspace mess, protected-path near miss, accidental public/private source mix-up, or failed file-operation rollback.

## Changelog

- 1.9.1 — 2026-05-27 — Captured the owner's runtime-category correction: `software-development/` should not be a catch-all; `hermes-proficiencies/` is the accepted temporary bucket for broad Hermes proficiency skills, while the larger OpenClaw-import taxonomy should be refined around domains of operation rather than vague artifact-class buckets. Why: the owner rejected the initial broad taxonomy proposal and asked to defer final naming/category design until more skills/SOPs are imported.
- 1.9 — 2026-05-27 — Reoriented skill source/runtime hygiene around the owner's new private runtime git repo model: tracked active/generated skills under `~/.hermes/skills/` are canonical for private local work, while `~/.hermes/skill-dev/` is reserved for public-bound/export work and hub/archive/metadata remain ignored. Why: the owner chose to make Hermes' installed skill folder the git-controlled working tree to eliminate private-source/runtime drift.
- 1.8 — 2026-05-27 — Refactored into a stronger progressive-disclosure / gradient design: moved mode-specific detail into support files, added a support-file map and shared verification template, and slimmed `SKILL.md` into a runtime contract + mode router + core workflow. Why: the owner wanted the skill to let Hermes move faster without making workspace messes; gradient design keeps common rules always visible while deeper guardrails load only when risk/complexity requires them.
- 1.7 — 2026-05-27 — Upgraded against `methodical-hermes-skill-tool-builder`: added explicit Runtime Contract, Expected Tools, Risk Classes, Mode Router, Local/Private Scope, Eval Cases, and related-skill routing updates. Why: adversarial review scored v1.6 at 19/26 and identified missing runtime-contract/eval/mode-router structure as the main blockers to preventing future workspace hygiene regressions while moving fast.
- 1.6 — 2026-05-27 — Added runtime skill category-selection rule and failure mode for using `software-development` as a catch-all. Why: the owner questioned why broad Hermes proficiencies were installed under `~/.hermes/skills/software-development/`; Hermes supports category folders, but category choice must be deliberate and based on artifact type/use-case, not the folder where the work happened.
- 1.5.1 — 2026-05-27 — Added `references/skill-dev-source-layout-regressions.md` and linked it from References. Why: the owner asked to actively capture the file-routing failure mode and learn the proper folder structure for future work; the detailed incident/audit checklist belongs in a support file while SKILL.md keeps the reusable rule.
- 1.5 — 2026-05-27 — Added flat private-proficiencies source layout rule: root-level `<skill-name>/` directories only, no redundant `skills/` or `software-development/` wrappers in `hermes-proficiencies`. Why: the owner identified the extra wrapper folders as another skill-dev routing regression; category folders belong in runtime install paths, not the private proficiencies source repo.
- 1.4 — 2026-05-27 — Added duplicate-source-repo placement guardrail for skill-dev hygiene and clarified runtime hotfix reconciliation must route to the correct source repo by artifact type, not always soulbound. Why: the owner corrected a regression where `tidy-hermes-workspace-hygiene` was copied into both the proficiencies repo and the soulbound/tool-skill repo; future audits should search sibling source repos and keep proficiencies out of soulbound even when both are private.
- 1.3 — 2026-05-26 — Added playbook-grade play sequence, thresholds, failure modes, review cadence, and changelog after adversarial scoring.
- 1.2 — 2026-05-26 — Added protected private knowledge-base wiki rule and Hermes skill source-of-truth rule.

## Common Pitfalls to Avoid

- Creating files in cwd or `~/.hermes/hermes-agent` by default.
- Treating “I'll organize it later” as acceptable.
- Performing significant file operations without git/status or another checkpoint.
- Retrying or working around a denied destructive/recursive file operation.
- Letting runtime/source skill copies drift or duplicate across repos.
- Loading all support files instead of following the mode router.

## References

- references/tidy-workspace-support-map.md — support-file router for progressive disclosure.
- references/modes/normal-workspace-hygiene.md — normal workspace/git/file-routing mode.
- references/modes/protected-wiki.md — protected wiki mode.
- references/modes/skill-source-runtime-hygiene.md — skill source/runtime and category mode.
- references/modes/destructive-operations.md — destructive/bulk operation mode.
- templates/workspace-verification-checklist.md — final verification checklist.
- references/openclaw-workspace-organization.md — Core three-tier model and folder taxonomy.
- references/openclaw-file-routing.md — Detailed routing SOP and naming conventions.
- references/skill-dev-source-layout-regressions.md — Skill-dev source repo layout rules, duplicate-placement regression pattern, and audit checklist.

This skill should be loaded automatically for any workspace-related work.
