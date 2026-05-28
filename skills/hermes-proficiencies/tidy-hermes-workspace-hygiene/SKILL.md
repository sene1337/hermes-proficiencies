---
name: tidy-hermes-workspace-hygiene
description: Use when Hermes is about to create, edit, move, delete, sync, route, publish, or leave behind durable files. Gives Hermes the tidy proficiency for git awareness, immediate file routing, and workspace hygiene so the agent does not make a mess.
version: 1.11.1
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [proficiency, tidy, workspace, git, file-management, hygiene, safety]
    related_skills: [methodical-hermes-skill-tool-builder, systematic-debugging, writing-plans, thorough-hermes-skill-publishing]
---

# Tidy Hermes Workspace Hygiene

## Overview

Prevent the agent from scattering files, performing destructive operations without safety nets, or violating the active workspace's organization and git practices. This skill encodes Hermes-native workspace discipline: route files before writing, use git as the safety net, and avoid agent-made messes.

## Core Philosophy

- Git is the primary safety net. Never rely on "I can undo it later."
- Route files at creation time. Never create orphans with the intention of filing them later.
- Respect existing systems. Follow the user's documented workspace rules unless explicitly told otherwise.
- Ask on ambiguity. When destination or risk level is unclear, stop and clarify.

## When to Use

Use this skill whenever Hermes is about to perform a file/workspace operation, whether or not the user explicitly asked for “workspace hygiene.” The trigger is the agent action, not just the user's wording.

Load it before:

- using `write_file`, `patch`, or terminal filesystem commands such as `cp`, `mv`, `rm`, `mkdir`, `rsync`, or generated-output writes;
- creating new documents, scripts, templates, support files, exports, packages, or review artifacts;
- editing, moving, deleting, overwriting, syncing, publishing, or leaving behind durable files;
- touching git state, source/runtime skill trees, public/shared repos, protected wiki paths, or cross-project workspaces;
- any operation that could create clutter, orphan files, source/runtime drift, or hard-to-reverse changes.

Do not use for: read-only answering with no file/workspace side effects, or purely internal Hermes temp work under `~/.hermes/tmp/` that is guaranteed to be cleaned in the same turn.

## Runtime Contract

### Invocation Contract

Hermes should load this skill before any agent action that can create, edit, move, delete, overwrite, route, publish, sync, or leave behind durable files. This is action-triggered: even if the user asks for a skill, plan, export, report, script, or cleanup without saying “file,” load this skill before Hermes writes or changes files. It also applies when a task touches git state, skill source/runtime trees, public/shared repositories, protected knowledge-base paths, or workspace organization decisions.

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
- editing protected knowledge-base paths;
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

Signal: installed skill tree, skill source repo, duplicate skill, source/runtime drift, or category placement
Mode: Skill source/runtime hygiene
Escalate: before deleting/moving/syncing skill directories or choosing a new taxonomy bucket

Signal: public/shared repo, GitHub push, packaging, or publish-clean copy
Mode: Publishing safety
Procedure: load thorough-hermes-skill-publishing before sync/push
Escalate: before any public write or remote change

Signal: protected wiki, personal knowledge base, shared docs, or other user-designated protected paths
Mode: Protected knowledge base
Procedure: references/modes/protected-wiki.md
Escalate: exact path + operation + reason + rollback plan before any write

Signal: rm, recursive delete, bulk move, overwrite, generated output over existing files
Mode: Destructive/bulk operation
Procedure: references/modes/destructive-operations.md
Escalate: always before execution unless explicitly pre-approved for exact scope

Signal: temp sweep, janitor audit, orphaned files, stale review bundles, workspace/tmp residue, non-canonical outputs, nightly cleanup cron
Mode: File janitor audit
Procedure: references/modes/file-janitor-audit.md
Escalate: only durable/valuable, sensitive, unlabeled, architecture-decision, or runtime-critical drift findings; scheduled runs should auto-tidy safe residue and ask the user for escalation decisions

Signal: new durable artifact with no destination
Mode: File routing
Procedure: references/modes/normal-workspace-hygiene.md file routing rules
Escalate: if taxonomy affects the user's operating system rather than a local implementation detail
```

## Portability Boundary

The default guidance in this file is portable: route before writing, check git/safety state, respect protected paths, and verify after changes. Local/private workspace policies belong in support files and must be stripped or parameterized before public export. Before publishing or sharing this skill, load `thorough-hermes-skill-publishing` and remove private paths, identities, repo names, chat IDs, internal changelogs, and machine-specific assumptions.

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
- `references/modes/skill-source-runtime-hygiene.md` — Hermes skill source/runtime, artifact-type category, duplicate, and private repo rules.
- `references/modes/destructive-operations.md` — delete/overwrite/bulk operation guardrails.
- `references/modes/file-janitor-audit.md` — temp sweep, orphan-file, stale review-bundle, and non-canonical residue classification/escalation mode.
- `templates/workspace-verification-checklist.md` — evidence checklist for final answers.

## Required Behaviors Summary

- Git is the primary safety net; check git state before significant edits.
- Route files at creation time; no durable orphan files in cwd/temp.
- Treat installed skills and skill source repos as high-impact workspaces: identify source of truth, inspect diffs, and avoid source/runtime drift.
- Use public/export staging only for publish-clean copies, packages, and release work; do not duplicate every private/local skill into public-bound workspaces.
- Choose runtime skill categories deliberately; avoid catch-all buckets unless explicitly accepted as temporary local policy.
- Treat protected knowledge bases as read-only unless exact write scope is approved.
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

User asks: “Create a project plan file,” “Patch this config,” “Move these notes,” or “Clean up this repo.” Hermes also triggers it internally when an apparently different task requires durable file writes, such as creating a skill support file, exporting a package, generating a report, or committing a runtime skill change.

Expected behavior: load this skill before the write/change, classify workspace, check git/safety state, choose final path before writing, use patch/write_file appropriately, and report touched paths + git/status evidence.

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

### Protected knowledge-base write

Task mentions protected wiki, personal knowledge base, shared docs, or other user-designated protected paths.

Expected behavior: read/search/summarize only by default. Before any write, present exact paths, operation, reason the protected path must be touched, and rollback plan.

### Tool unavailable / no git repo

Git is unavailable, the path is not in a repo, or git status cannot be checked.

Expected behavior: say the safety check failed, avoid claiming git evidence, and ask before significant durable changes unless another explicit checkpoint exists.

### Runtime/source skill hygiene

User asks to edit an installed skill, fix source/runtime drift, or review a skill source/export folder regression.

Expected behavior: identify whether the artifact is an installed runtime copy, private/local source copy, or public-bound package; inspect plausible source locations for duplicates; patch the canonical private source/runtime tree according to local policy; sync/export only after source is correct and overwrite scope is safe.

### Neighboring-skill collision

User asks to publish a skill, author a new Hermes skill, write a human SOP, or debug code.

Expected behavior: load the neighboring governing skill (`thorough-hermes-skill-publishing`, `methodical-hermes-skill-tool-builder`, `helpful-hermes-human-playbook-sop-creator`, `systematic-debugging`) and keep this skill focused on file routing/safety.

## Failure Modes

- **Failure:** Agent creates files in cwd because it is convenient or because the user did not explicitly ask for workspace hygiene.
  **Fix:** Treat file creation/editing as the trigger. Stop, identify final path, move/recreate in the correct location, and verify no orphan remains.

- **Failure:** Agent treats broad project instructions as permission to edit protected knowledge-base files.
  **Fix:** Default to read/search/summarize; require exact path/operation/reason/rollback approval before writing.

- **Failure:** Agent edits an installed/runtime skill and forgets source of truth.
  **Fix:** Identify the active local source/runtime policy, inspect diffs, and reconcile the change before calling the source clean.

- **Failure:** Agent uses a catch-all runtime category or proposes vague taxonomy buckets before the domain structure is clear.
  **Fix:** Classify by domain of operation and artifact use-case first. Keep broad taxonomy decisions explicit and reversible until enough skills/SOPs are classified.

- **Failure:** Agent claims git/source/runtime validation without evidence.
  **Fix:** Report actual git root/status/equality checks or explicitly state what was not verified.

- **Failure:** Agent loads every support file by default.
  **Fix:** Follow the mode router; load only the selected mode file and shared checklist unless deeper detail is necessary.

## Review Cadence

Review this skill monthly while workspace/proficiency behavior is actively changing, then quarterly once stable. Review immediately after any workspace mess, protected-path near miss, accidental public/private source mix-up, or failed file-operation rollback.

## Common Pitfalls to Avoid

- Creating files in the current working directory by default.
- Treating “I'll organize it later” as acceptable.
- Performing significant file operations without git/status or another checkpoint.
- Retrying or working around a denied destructive/recursive file operation.
- Letting runtime/source skill copies drift or duplicate across repos.
- Loading all support files instead of following the mode router.

## References

- references/tidy-workspace-support-map.md — support-file router for progressive disclosure.
- references/modes/normal-workspace-hygiene.md — normal workspace/git/file-routing mode.
- references/modes/protected-wiki.md — protected knowledge-base mode.
- references/modes/skill-source-runtime-hygiene.md — skill source/runtime and category mode.
- references/modes/destructive-operations.md — destructive/bulk operation mode.
- references/modes/file-janitor-audit.md — janitor/temp-residue classification and escalation mode.
- templates/workspace-verification-checklist.md — final verification checklist.
- references/workspace-organization-reference.md — local/source reference for workspace taxonomy.
- references/file-routing-reference.md — local/source reference for file-routing and naming rules.

This skill should be loaded automatically before any agent file/workspace operation so Hermes does not make a mess.
