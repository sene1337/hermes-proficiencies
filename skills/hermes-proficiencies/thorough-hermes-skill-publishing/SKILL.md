---
name: thorough-hermes-skill-publishing
description: Use when preparing to share or publish a Hermes skill. Gives Hermes the thorough proficiency for runtime validation, portability checks, safe syncing, artifact hygiene, and private-data leak prevention.
version: 1.6.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [proficiency, thorough, skills, publishing, distribution, safety, portability]
    related_skills: [methodical-hermes-skill-tool-builder, hermes-agent-skill-authoring, tidy-hermes-workspace-hygiene]
---

# Thorough Hermes Skill Publishing

## Overview

Install the **thorough publishing** proficiency: Hermes prevents private data, machine-specific assumptions, unverified behavior, and messy artifacts from crossing the boundary between private/runtime skills and public/shared/publishable skills.

This is a publishing gate, not a general skill-authoring standard. It answers:

```text
Is this skill safe, portable, clean, and evidenced enough to share?
```

Keep this `SKILL.md` as the runtime router. Load support files only for the selected mode.

## When to Use

Use this skill when:

- preparing to push a skill to a public or shared repository;
- extracting a live runtime/private skill into a publish-clean artifact;
- checking a skill package, archive, release, or shared copy for private-data leaks;
- syncing a runtime/private skill into `~/.hermes/skill-dev/` or another publish/export workspace;
- deciding whether a skill is publish-ready, private-only, owner-review-required, or blocked;
- handling a sensitive-data publishing incident.

Do not use for:

- private-only skill work with no publish/share/export intent;
- creating or scoring agent-runtime quality in general — use `methodical-hermes-skill-tool-builder`;
- Hermes frontmatter/validator mechanics alone — use `hermes-agent-skill-authoring`;
- generic file cleanup or workspace routing alone — use `tidy-hermes-workspace-hygiene`;
- human-facing playbooks/SOPs that are not Hermes skills — use `helpful-hermes-human-playbook-sop-creator`.

## Neighbor Routing

```text
Create/review runtime skill quality
→ methodical-hermes-skill-tool-builder

Skill syntax/frontmatter/validator conventions
→ hermes-agent-skill-authoring

Any publishing work that creates, copies, edits, deletes, commits, packages, or touches repos/files
→ also load tidy-hermes-workspace-hygiene

Human-facing Playbook/SOP artifact
→ helpful-hermes-human-playbook-sop-creator

Public/shared release safety, leak checks, portability, export hygiene, publish approval
→ thorough-hermes-skill-publishing
```

This skill owns public/private release safety. Tidy owns workspace mess prevention. Methodical owns runtime skill quality.

## Runtime Contract

Hermes may autonomously:

- inspect skill files, support files, package contents, git status, diffs, and remotes;
- run read-only scans for private paths, identifiers, secrets, user names, local-only references, `.git/` leakage, and internal changelogs;
- run non-mutating validation/test commands;
- classify the artifact as `publish-ready`, `ready after listed fixes`, `owner-review-required`, `private-only`, or `blocked`;
- draft a readiness report, export plan, remediation list, or rollback plan.

Hermes must ask before:

- copying/syncing files into a publishable repo;
- editing publishable artifacts or public docs;
- deleting staging directories or package artifacts;
- running `git add`, `git commit`, `git push`, release creation, package upload, or other public/shared writes;
- writing private daily logs or incident logs;
- force-pushing, rewriting history, deleting releases, or taking destructive rollback actions.

Stop immediately when:

- runtime/private/public source boundaries are unclear;
- repo remote or privacy boundary cannot be verified;
- likely secrets, chat IDs, personal details, or private paths are found and remediation is not approved;
- a public artifact would present local/private policy as portable guidance;
- publish evidence cannot be collected but the user asks to publish anyway.

## Risk Classes

```text
Publish-readiness review only
  Read-only. Produce evidence, verdict, and fixes. No edits by default.

Runtime-to-publish export planning
  Medium risk. Identify source/destination, scan, and plan. Ask before copy/sync.

Safe sync / repo preparation
  High risk. Requires path/remote/status checks and before/after diff review.

Package/release hygiene
  Medium-to-high risk. Inspecting packages is safe; release/upload is approval-gated.

Public publish gate
  High-impact external side effect. Requires complete evidence and explicit approval.

Sensitive-data incident rollback
  Emergency/destructive risk. Prioritize containment, credential rotation, and scoped owner approval.
```

## Mode Router

Choose the mode before touching files or repos.

```text
Signal: “review before publishing”, “is this safe to share?”, “publish-ready?”
Mode: Publish-readiness review only
Support: templates/publish-readiness-report.md + references/checklists/pre-publish-evidence.md
Action: read-only audit, verdict, fixes; no edits by default

Signal: runtime/private skill should become public/shared
Mode: Runtime-to-publish export planning
Support: references/checklists/private-data-scan.md + templates/publish-readiness-report.md
Action: identify source/destination, scan, plan remediation; ask before copy/sync

Signal: copy/sync/export into skill-dev/public repo
Mode: Safe sync / repo preparation
Support: references/checklists/pre-publish-evidence.md
Action: verify path/remote/status, diff before/after, selective copy only after approval

Signal: package/archive/release artifact
Mode: Package/release hygiene
Support: references/checklists/pre-publish-evidence.md
Action: inspect file list, `.git` leakage, staging dirs, generated files; ask before upload

Signal: “push it”, “publish it”, “make release”
Mode: Public publish gate
Support: templates/publish-readiness-report.md
Action: verify evidence, summarize approval scope, wait for explicit public-write approval

Signal: private data/credential/chat/path leaked or already pushed
Mode: Sensitive-data incident rollback
Support: references/modes/sensitive-data-rollback.md
Action: contain, rotate if needed, revert/delete/rewrite only with scoped approval

Signal: post-publish cleanup/logging
Mode: Cleanup and private logging
Support: tidy-hermes-workspace-hygiene + references/checklists/pre-publish-evidence.md
Action: clean only approved artifacts; log privately only if user/workflow asks
```

## Core Principles

- **Private development, public publishing.** Work privately; publish only reviewed artifacts.
- **Runtime first, publish second.** Live behavior should be proven before export.
- **Live success does not equal publish-clean.** Behavior, portability, privacy, and package hygiene are separate gates.
- **Diff before sync.** Never blindly copy or overwrite runtime/private trees into publishable repos.
- **Private data has no place in shared skills.** Assume anything committed, packaged, or pushed can be read by strangers.
- **Evidence beats confidence.** Publish-readiness claims require visible checks.
- **Approval gates survive good evidence.** Passing scans does not authorize public writes.

## Local / Private Policy Boundary

The user's active private/local skill work happens in the git-controlled runtime skill library at `~/.hermes/skills/` when the skill is actively worked on or generated/agent-created. `~/.hermes/skill-dev/` is reserved for public/shared release, publish-clean export, or package/release work.

Canonical lifecycle:

```text
private runtime skill library in ~/.hermes/skills/
→ live Hermes validation on the installed skill
→ publish-clean export/review in ~/.hermes/skill-dev/ or a public/shared repo
→ public/shared push only after publishing gate evidence and explicit approval
```

Public artifacts must not include user-specific names, private paths, repo names, chat IDs, memory paths, daily-log assumptions, internal changelog notes, or local architecture rules unless the artifact is explicitly labeled private/local and is not being published.

## Compact Publishing Procedure

1. **Pin the artifact and boundary.** Record source path, version, runtime/private/public/pasted/package classification, destination, and audience.
2. **Verify repo safety.** For any repo: `pwd`, `git status --short`, `git remote -v`. Stop if path, remote, or privacy boundary is unclear.
3. **Validate runtime behavior.** Confirm live behavior, validator output, tests, or reproducible manual steps before treating runtime success as exportable.
4. **Run private-data scan.** Use `references/checklists/private-data-scan.md`. Prefer redacted findings; do not paste secrets into chat.
6. **Check portability.** Remove, parameterize, or mark private-only any local paths, profile assumptions, private repo names, account IDs, and machine-specific setup.
7. **Sync only after approval.** Load tidy first. Diff before copy, copy selectively, then inspect diff/status after copy.
8. **Check package/release hygiene.** Use `references/checklists/pre-publish-evidence.md` for archive lists, `.git/` leakage, staging wrappers, generated files, README/docs, and examples.
9. **Gate public write.** Present exact repo/path/remote, exact operation, evidence, unresolved risks, and what will not be touched. Wait for explicit scoped approval.
10. **Handle timeout/stall safely.** If approval expires, stop without pushing, preserve prepared state, and report the exact resume phrase/context.
11. **Cleanup privately.** Clean only approved staging/build artifacts. Write private logs only when the user/workflow asks; never include private logs in published artifacts.

## Minimum Verification Evidence

Use `references/checklists/pre-publish-evidence.md` for detailed checks and `templates/publish-readiness-report.md` for output shape.

Minimum final evidence:

- **Artifact:** name, version, source path, support files included.
- **Boundary:** runtime/private/public classification, destination, `pwd`, `git status --short`, `git remote -v` when applicable.
- **Diff:** files changed/copied/deleted, diff reviewed, no blind sync.
- **Private-data scan:** path/name/ID/secret/private-file checks and unresolved findings.
- **Portability:** local assumptions removed, parameterized, or marked private-only.
- **Runtime/validation:** live behavior/test/validator evidence or explicit deferral.
- **Package:** archive/file-list and `.git/` absence when package/release exists.
- **Final verdict:** `publish-ready`, `ready after listed fixes`, `owner-review-required`, `private-only`, or `blocked`.
- **Approval:** explicit scoped approval before any public/shared write.

Do not claim publish readiness, repo cleanliness, source/runtime equality, package hygiene, or public safety unless those checks were performed in this turn or are visible in current context.

## Private-Data Scan Minimums

Always check the artifact and included support files for:

- local paths and profile-specific Hermes assumptions;
- personal names, family names, org names, account handles, emails, phone numbers;
- chat/platform IDs, webhook URLs, tokens, passwords, private keys, cookies, bearer strings;
- vault/item names, secret-manager paths, memory files, daily logs, private notes;
- private repo names, private source-system names, local architecture, and internal maintenance rationale.

Remediate by removing, parameterizing, moving to a private reference, labeling private-only, or blocking publish. Secrets block publish and require rotation if exposed.

## Sensitive-Data Incident Summary

When private data may have reached a shared/public surface:

1. Stop further publishing or syncing.
2. Pin what leaked and where it went without reprinting secrets.
3. Contain with the least-destructive option that works.
4. Rotate credentials if secrets/webhooks/tokens may be exposed.
5. Use destructive history rewrite or release deletion only with exact scoped approval.
6. Verify the clean current tree/package and report remaining cached/out-of-control exposure.

Load `references/modes/sensitive-data-rollback.md` for the full procedure.

## Eval Cases

Keep evals out of the default path. Load `references/eval-cases.md` when changing this skill, checking invocation behavior, or reviewing whether a past publishing run followed the standard.

Critical eval signals:

- publish review → read-only evidence and verdict, no edits by default;
- runtime-to-public export → load tidy, verify source/destination/remote, ask before copy;
- package leak check → inspect file list and block on private data or `.git` leakage;
- skill construction or frontmatter-only question → route to neighboring skill instead;
- public write → present exact approval scope and wait;
- sensitive leak/force-push request → incident mode with credential rotation and scoped destructive approval;
- timed approval expiry → do not push or mutate; report resume context.

## Parent Feedback / Observed-Use Loop

Patch reusable publishing/privacy/package/approval/rollback gaps into this skill. Route runtime-quality gaps to `methodical-hermes-skill-tool-builder`, frontmatter gaps to `hermes-agent-skill-authoring`, workspace/source gaps to `tidy-hermes-workspace-hygiene`, and human Playbook/SOP confusion to `helpful-hermes-human-playbook-sop-creator`.

Capture reusable procedure or failure mode, not transient repo names, commit SHAs, PR numbers, or incident narrative.

## Common Pitfalls

Top failures: treating live behavior as publish-ready, blind runtime-to-public sync, leaking private policy/changelogs/logs, using public repos as scratchpads, pushing the full runtime library, shipping `.git`/staging junk, skipping approval, mutating after approval timeout, destructive rollback before containment/rotation, and verification overclaim.

## Support Files

- `references/checklists/pre-publish-evidence.md` — detailed publish-readiness, sync, package, and public-write evidence checklist.
- `references/checklists/private-data-scan.md` — scan targets and remediation choices for local paths, IDs, secrets, private files, and personal context.
- `references/modes/sensitive-data-rollback.md` — emergency response for private data or credentials that reached a shared/public surface.
- `references/eval-cases.md` — full eval cases for invocation, export, package leak checks, approval gates, and incident rollback.
- `templates/publish-readiness-report.md` — copyable output report shape.
- `references/skill-publishing-source-reference.md` — source-lineage reference from the original source Skill Publishing SOP.

## Verification Checklist

Before calling a skill publish-ready:

- [ ] Artifact pinned by path, version, and source classification.
- [ ] Runtime behavior validated or explicitly deferred with reason.
- [ ] Destination repo/path/remote and privacy boundary verified.
- [ ] Git status/diff evidence reviewed before and after sync/copy.
- [ ] Private-data scan run across `SKILL.md` and support/package files.
- [ ] Local/profile-specific assumptions removed, parameterized, or labeled private-only.
- [ ] Internal changelog notes excluded from public export.
- [ ] Support files and package contents checked, not just `SKILL.md`.
- [ ] Archive/release artifacts contain no `.git/` leakage or staging junk.
- [ ] Workspace hygiene completed after export/package work.
- [ ] Public write approval explicit and scoped.
- [ ] Final verdict matches actual evidence.

This skill should be loaded whenever preparing a Hermes skill for distribution.
