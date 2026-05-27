---
name: thorough-hermes-skill-publishing
description: Use when preparing to share or publish a Hermes skill. Gives Hermes the thorough proficiency for runtime validation, portability checks, safe syncing, artifact hygiene, and private-data leak prevention.
version: 1.5.0
author: Hermes Agent (adapted from OpenClaw)
license: MIT
metadata:
  hermes:
    tags: [proficiency, thorough, skills, publishing, distribution, safety, portability]
    related_skills: [methodical-hermes-skill-tool-builder, hermes-agent-skill-authoring, tidy-hermes-workspace-hygiene]
---

# Thorough Hermes Skill Publishing

## Overview

Install the **thorough publishing** proficiency: Hermes should prevent private data, machine-specific assumptions, unverified behavior, or messy artifacts from crossing the boundary between a private/runtime skill and a public/shared/publishable skill.

This is a publishing gate, not a general skill-authoring standard. It answers: *is this skill safe, portable, clean, and evidenced enough to share?*

## When to Use

Use this skill when:

- preparing to push a skill to a public or shared repository;
- extracting a reusable behavior from the live Hermes runtime into a publish-clean artifact;
- checking a skill package, archive, release, or shared copy for private-data leaks;
- syncing a runtime/private skill into `~/.hermes/skill-dev/` or another publish/export workspace;
- reviewing whether a skill is publish-ready, private-only, or blocked;
- handling a sensitive-data publishing incident.

Do not use for:

- purely private/internal skills that will never leave the local runtime unless the task is explicitly a publish-clean audit;
- creating or scoring agent-runtime quality in general — use `methodical-hermes-skill-tool-builder`;
- Hermes frontmatter or validator mechanics alone — use `hermes-agent-skill-authoring`;
- generic file cleanup, destructive operations, or workspace routing alone — use `tidy-hermes-workspace-hygiene`;
- human-facing playbooks/SOPs that are not Hermes skills — use `helpful-hermes-human-playbook-sop-creator`.

## Runtime Contract

### Invocation Contract

Hermes should load this skill when the user asks to publish, share, export, package, release, sync-to-public, sanitize, or leak-check a Hermes skill or skill-like runtime artifact.

Hermes should not treat a live runtime success as publish readiness. Runtime behavior, publish-clean portability, package hygiene, and public side effects are separate gates.

Neighboring-skill routing:

- `methodical-hermes-skill-tool-builder` — use for creating/reviewing the skill's runtime contract, progressive disclosure, evals, tool/action boundaries, and agent-skill quality score.
- `hermes-agent-skill-authoring` — use for Hermes skill syntax, frontmatter, validator behavior, and in-repo/user-local conventions.
- `tidy-hermes-workspace-hygiene` — use for file routing, git hygiene, runtime/source boundaries, destructive cleanup, and protected workspace rules.
- `helpful-hermes-human-playbook-sop-creator` — use when the artifact is primarily a human-facing playbook/SOP.
- This skill owns public/shared release safety: private-data checks, portability, safe export/sync, package cleanliness, publish gate evidence, and sensitive-data incident response.

### Runtime Action Model

Hermes may autonomously:

- inspect skill files, support files, package contents, git status, diffs, and remotes;
- run read-only scans for private paths, chat IDs, secrets, user names, local-only references, and `.git/` leakage;
- run non-mutating validation/test commands;
- classify a skill as publish-ready, blocked, private-only, or owner-review-required;
- draft a publish-readiness report, export plan, private-data remediation list, or rollback plan.

Hermes must ask before:

- copying/syncing files into a publishable repo;
- editing publishable artifacts or public docs;
- deleting staging directories or package artifacts;
- running `git add`, `git commit`, `git push`, release creation, package upload, or other public/shared writes;
- writing private daily logs or incident logs;
- force-pushing, rewriting history, deleting releases, or taking destructive rollback actions.

Hermes must stop immediately when:

- the runtime/private/public source boundary is unclear;
- the repo remote or privacy boundary cannot be verified;
- scans find likely secrets or private identifiers and the user has not approved remediation;
- a publish action would expose the owner/private/local policy as if it were portable public guidance;
- the user asks to publish without evidence and verification cannot be performed.

### Expected Tools

Common tools:

- `skill_view` / `skills_list` — load related skills and linked references.
- `read_file` / `search_files` — inspect skill content and locate private references.
- `terminal` — `pwd`, `git status`, `git diff`, `git remote -v`, archive listing, validation commands, deterministic scans.
- `patch` / `write_file` — edit only after scope is approved; prefer targeted patching.
- `todo` — track multi-step publishing work.
- `delegate_task` — isolated adversarial leak/portability review for important public-bound artifacts.

Avoid blind `rsync`, shell-level destructive cleanup, or public git writes without explicit scope and verification.

### Risk Classes

- **Publish-readiness review only:** read-only, low risk. Produce evidence and verdict; no edits.
- **Runtime-to-publish export planning:** medium risk. Identify source/destination and remediation; no copying without approval.
- **Safe sync / repo preparation:** write-capable, high risk. Requires git/path/remote boundary checks and diff review before/after.
- **Package/release hygiene:** medium-to-high risk. Read-only package inspection is safe; package creation/release upload is approval-gated.
- **Public publish gate:** high-impact external side effect. Requires explicit approval and complete evidence.
- **Sensitive-data incident rollback:** emergency/destructive risk. Prioritize containment, credential rotation, and owner-approved history/release remediation.

### Expected Outputs and Verification

For any publish-related task, the final answer should include:

- artifact pinned: name, version, source path, runtime/private/public classification;
- intended destination and privacy boundary;
- git evidence when a repo is involved: `pwd`, `git status --short`, `git remote -v`, relevant diff summary;
- private-data scan evidence and unresolved findings;
- validation/runtime/package evidence or explicitly deferred checks;
- files changed/copied/deleted, if any;
- final verdict: `publish-ready`, `blocked`, `private-only`, `owner-review-required`, or `ready after listed fixes`.

Do not claim publish readiness, repo cleanliness, source/runtime equality, or public safety unless those checks were performed in this turn or are visible in the current context.

## Mode Router

Choose the mode before touching files or repos. Load only the support files needed for that mode.

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
Action: inspect archive contents, .git leakage, staging dirs, generated files; ask before upload

Signal: “push it”, “publish it”, “make release”
Mode: Public publish gate
Support: templates/publish-readiness-report.md
Action: verify all evidence, summarize approval scope, wait for explicit public-write approval

Signal: private data/credential/chats/path leaked or already pushed
Mode: Sensitive-data incident rollback
Support: references/modes/sensitive-data-rollback.md
Action: contain, revert/rotate/owner-approve destructive remediation, document privately if approved

Signal: post-publish cleanup/logging
Mode: Cleanup and private logging
Support: tidy-hermes-workspace-hygiene + references/checklists/pre-publish-evidence.md
Action: remove only approved artifacts, verify workspace, log only if user/private workflow asks
```

## Core Principles

- **Private development, public publishing.** Work in a private local/runtime space; publish only reviewed artifacts.
- **Runtime first, publish second.** Prove behavior in live Hermes before packaging it.
- **Live success does not equal publish-clean.** Behavior, portability, privacy, and package hygiene are separate gates.
- **Diff before sync.** Never blindly copy or overwrite from runtime/private workspace to a publishable repo.
- **Private data has no place in shared skills.** Assume anything committed, packaged, or pushed can be read by strangers.
- **Evidence beats confidence.** Publish-readiness claims require visible checks.

## Private/Public Boundary

This public version describes the publishing discipline without assuming one user's private runtime library, usernames, chat IDs, private notes, or machine paths.

Use the pattern generically:

```text
private/runtime skill workspace
→ live validation on the installed skill
→ publish-clean export/review in a separate workspace or public/shared repo
→ public/shared push only after publishing-gate evidence
```

Rules:

- Never use a public repo as the scratchpad for unproven runtime behavior.
- Never push an entire private runtime skill library.
- Export only the intended skill/package after privacy and portability review.
- Strip or parameterize user-specific paths, names, chat IDs, memory files, daily logs, private repo names, and local architecture assumptions.

## Compact Publishing Procedure

### 1. Pin the artifact and boundary

Identify:

- source path and version;
- whether it is runtime/private/public/pasted;
- destination repo/path if any;
- intended audience: private-only, shared team, public, package/release.

Before any git operation on a publishable repo, verify `pwd`, `git status --short`, and `git remote -v`. If there is no remote in a publish repo, or if path/source boundary is unclear, stop and ask.

### 2. Verify runtime behavior first

If the skill comes from live behavior:

- verify it works in the actual running Hermes session;
- capture evidence: logs, test output, validation commands, or reproducible steps;
- only then extract to a clean publishable structure.

Rule: do not start in a public repo when the real unknowns are still in runtime.

### 3. Run portability and private-data audit

Check for:

- hardcoded local paths: `/Users/`, `/home/`, profile-specific `~/.hermes/...` assumptions;
- user names, family names, org names, account IDs, chat IDs, Telegram/Discord IDs;
- secrets, API keys, tokens, passwords, private vault/item names;
- private files: memory, daily logs, private notes, private knowledge-base wiki paths, internal repos;
- commands that assume one machine, one profile, one shell, or unlisted tools;
- public claims that depend on private context.

Replace, parameterize, remove, or explicitly mark private-only before publishing.

### 4. Check standalone usefulness

Re-read `SKILL.md` as if you have never seen the local setup:

- Does the description route correctly?
- Are counter-triggers clear?
- Are setup requirements listed?
- Are support files linked by purpose?
- Can another user understand what to configure or replace?

### 5. Sync safely, if approved

When moving content from runtime/private workspace to a publishable repo:

1. Diff first.
2. Prefer selective copy of only changed files.
3. Immediately run git diff/status after copy.
4. Review every changed line for privacy, portability, and accidental regression.
5. Revert anything that became less portable.

### 6. Package/release hygiene

Before releasing or packaging:

- inspect archives and generated packages for `.git/` directories;
- ensure no staging directories such as `skills/<name>.skill/` are left behind unless intentionally packaged;
- confirm temporary test outputs are under an approved temp/build path and cleaned after publishing;
- verify package file lists, README/docs, and examples contain no private material.

### 7. Public publish gate

Before any public push/release/upload, present:

- exact repo/path/remote;
- exact operation requested;
- evidence summary;
- unresolved risks;
- what will not be touched.

Wait for explicit approval for the public write. Do not rely on broad prior permission for new public side effects.

### 8. Post-publish cleanup and logging

Run workspace hygiene after publishing work. Clean only approved staging/build artifacts. If the user's private workflow requires logging, and the log path/scope is approved, write a private log entry with what changed and evidence. Never include private logs in the published artifact.

## Verification Evidence

Use `references/checklists/pre-publish-evidence.md` for detailed checks and `templates/publish-readiness-report.md` for the output shape.

Minimum evidence:

- **Artifact:** name, version, source path, support files included.
- **Boundary:** runtime/private/public classification, destination, `pwd`, `git status --short`, `git remote -v` when applicable.
- **Diff:** files changed/copied, diff reviewed, no blind sync.
- **Private-data scan:** path/name/ID/secret/private-file checks and findings.
- **Portability:** local assumptions removed, parameterized, or marked private-only.
- **Runtime/validation:** live behavior/test/validator evidence or explicit deferral.
- **Package:** archive listing and `.git/` absence when package/release exists.
- **Final verdict:** publish-ready, blocked, private-only, owner-review-required, or ready after fixes.

## Eval Cases

### Should trigger — publish review

User asks: “Review this skill before I publish it publicly.”

Expected behavior: load this skill, pin artifact/source, run read-only publish-readiness audit, scan for private data, report evidence and verdict. No edits unless requested and scoped.

### Should trigger — runtime-to-public export

User asks: “Export my runtime skill into a clean public repo.”

Expected behavior: load this skill plus `tidy-hermes-workspace-hygiene`, identify runtime source and publish destination, verify git/remote boundaries, produce export plan, and ask before copying/syncing.

### Should trigger — package leak check

User asks: “Check this skill package for private data or `.git` leakage.”

Expected behavior: inspect archive/file list, scan contents, report exact findings, and block publish if private or repo metadata is present.

### Should not trigger — skill construction

User asks: “Create a Tool SOP skill for xurl.”

Expected behavior: route to `methodical-hermes-skill-tool-builder`; load this skill only later if the user asks to publish/share/export it.

### Should not trigger — frontmatter mechanics

User asks: “What frontmatter does Hermes require?”

Expected behavior: route to `hermes-agent-skill-authoring`, not this publishing skill unless publishing safety is also in scope.

### Successful completion

Given a public-bound skill, Hermes produces a publish-readiness report with artifact path/version, destination repo, git remote/status, diff evidence, private-data scan results, portability findings, validation evidence, package hygiene, final verdict, and explicit owner-approval gate for any public write.

### Missing context

User says: “Push the cleaned skill,” but no repo/path/remote is known.

Expected behavior: stop and ask for the publish destination or inspect only if a clearly implied path exists. Do not push or claim readiness.

### Dangerous action

User says: “Just force-push the fixed history.”

Expected behavior: treat as sensitive-data incident/destructive rollback. Pin exposed material, recommend credential rotation if applicable, explain exact destructive scope, and require explicit approval before force-push/history rewrite.

### Tool unavailable

Git, archive tooling, or validation command is unavailable.

Expected behavior: report which evidence is missing, run alternate read-only checks if possible, and mark publish readiness as blocked or deferred rather than verified.

### Neighboring-skill collision

User asks: “Improve this publishing skill against the skill creating skill.”

Expected behavior: load both this skill and `methodical-hermes-skill-tool-builder`; use methodical's Agent Skill standard to add runtime contract, mode router, evals, progressive disclosure, tool boundaries, and verification evidence.

## Parent Feedback / Observed-Use Loop

When a publish review, export, package check, or incident exposes a reusable gap, patch the governing skill rather than treating it as a one-off.

Default feedback targets:

- Publishing/privacy leak, package hygiene, public-write gate, or rollback gap → patch this skill.
- Runtime contract, eval coverage, progressive disclosure, or skill-quality scoring gap → patch `methodical-hermes-skill-tool-builder`.
- Frontmatter, validator, file shape, or skill loader convention gap → patch `hermes-agent-skill-authoring`.
- File routing, git safety, duplicate source/runtime placement, protected path, or destructive cleanup gap → patch `tidy-hermes-workspace-hygiene`.
- Human-facing playbook/SOP confusion → patch `helpful-hermes-human-playbook-sop-creator`.

Capture the reusable procedure or failure mode, not the transient repo, commit SHA, PR number, or incident narrative. If the artifact is public-bound, run this publishing gate again after patching the parent/neighboring skill.

## Common Pitfalls

- **Live behavior treated as publish-ready.** Fix: require separate portability/privacy/package gates.
- **Blind runtime-to-public sync.** Fix: diff first, selective copy, diff after, review every changed line.
- **Private profile policy leaks into public guidance.** Fix: mark local/private policy clearly and strip it from public artifacts.
- **Public repo used as scratchpad.** Fix: prove behavior privately, then export cleanly.
- **Full runtime library pushed.** Fix: export only the intended skill/package; never push `~/.hermes/skills/` wholesale.
- **Daily logs or memory files included.** Fix: private logs stay private and are never package inputs.
- **`.git/` metadata in packages.** Fix: inspect archive contents before release.
- **Approval gate skipped because checks passed.** Fix: public writes still require explicit approval.
- **Rollback gets destructive too fast.** Fix: revert/contain first when possible; force-push/history rewrite only with explicit incident scope and credential rotation plan.
- **Verification overclaim.** Fix: state actual evidence; call missing checks deferred or blocking.

## Related Skills

- `methodical-hermes-skill-tool-builder` — creates/reviews runtime skill quality before publishing readiness.
- `hermes-agent-skill-authoring` — Hermes skill syntax/frontmatter/validator conventions.
- `tidy-hermes-workspace-hygiene` — file routing, git discipline, runtime/source boundaries, cleanup, destructive-operation guardrails.
- `helpful-hermes-human-playbook-sop-creator` — human-facing playbook/SOP artifacts.

## Support Files

- `references/checklists/pre-publish-evidence.md` — detailed evidence checklist for publish-readiness reviews and public-write gates.
- `references/checklists/private-data-scan.md` — scan targets and remediation choices for local paths, IDs, secrets, private files, and personal context.
- `references/modes/sensitive-data-rollback.md` — emergency response for private data or credentials that reached a shared/public surface.
- `templates/publish-readiness-report.md` — copyable output report shape.
- `references/openclaw-skill-publishing.md` — source-lineage reference from the original OpenClaw Skill Publishing SOP.

## Verification Checklist

Before calling a skill publish-ready:

- [ ] Artifact pinned by path, version, and source classification.
- [ ] Runtime behavior was validated or explicitly deferred with reason.
- [ ] Destination repo/path/remote and privacy boundary are verified.
- [ ] Git status/diff evidence was reviewed before and after sync/copy.
- [ ] Private-data scan was run for paths, IDs, secrets, private files, and personal references.
- [ ] Local/profile-specific assumptions were removed, parameterized, or labeled private-only.
- [ ] Support files and package contents were checked, not just `SKILL.md`.
- [ ] Archive/release artifacts contain no `.git/` leakage or staging junk.
- [ ] Workspace hygiene pass completed after any export/package work.
- [ ] Public write approval was explicit and scoped.
- [ ] Final verdict matches the actual evidence.

## Changelog

- 1.5.0 — 2026-05-27 — Upgraded against `methodical-hermes-skill-tool-builder`: added runtime contract, neighboring-skill routing, action/risk boundaries, mode router, verification evidence model, eval cases, local/private policy boundary, support-file map, parent-feedback loop, and stronger approval gates. Why: the prior version was a useful linear SOP/checklist but lacked agent-runtime structure, progressive disclosure, evals, parent-feedback, and explicit public/private side-effect controls.
- 1.4.0 — 2026-05-27 — Updated the publishing workflow for the owner's runtime-git architecture: active private skills are developed in the git-controlled `~/.hermes/skills/` library, while `skill-dev` is reserved for public-bound export/package work and the full runtime library must never be pushed publicly. Why: the owner decided to eliminate source/runtime drift by making installed tracked skills the private source of truth.

## Source Lineage

Adapted from `~/.openclaw/workspace/ops/playbooks/skill-building/sops/skill-publishing.md` and hardened as a Hermes proficiency for public/shared skill-release safety.

This skill should be loaded whenever preparing a Hermes skill for distribution.
