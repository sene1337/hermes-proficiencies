# File Janitor Audit Mode

Use this mode when the task is not creating a file right now, but auditing existing filesystem residue: temp directories, workspace `tmp/`, review bundles, orphaned outputs, duplicated artifacts, stale build/package products, or non-canonical files that may need routing or cleanup.

## Purpose

Tidy behavior is prevention; file janitor behavior is detection and triage. This mode catches what prevention missed without turning every temp file into a human decision.

## Canonical Inputs

Before auditing, identify the workspace's current routing policy and scan scope. Prefer a single stable policy index if the workspace has one, so scheduled prompts do not hardcode fragile SOP paths.

Minimum policy inputs:

- workspace taxonomy / organization rules;
- file-routing SOP or equivalent;
- audit-artifact typeification rules;
- protected/private path rules;
- destructive cleanup approval policy.

## Classification Model

Classify findings before escalating:

- `scratch` — throwaway probe, transient log, cache, screenshot, command output. Usually safe to ignore/trash.
- `reproducible` — clone, download, generated output, build product, or package that can be recreated. Usually safe to trash unless locally modified or costly to reproduce.
- `review-staged` — temporary review bundle, extracted package, side-by-side comparison, or patch package. Safe to trash after review unless accepted/promoted; should carry source/purpose context.
- `durable` — unique or valuable output that belongs in a canonical workspace path. Route or escalate.
- `unlabeled` — unclear residue. Treat as a process failure; inspect enough to classify or escalate.

## Scan Scope Pattern

Common scopes:

- workspace root and workspace `tmp/`;
- system temp paths such as `/tmp` and `/private/tmp`;
- known non-workspace operational paths where agents or tools often leave residue;
- active runtime paths that must never point into system temp.

Do not broaden scans into protected personal knowledge bases, credential stores, or unrelated home-directory trees unless the user approved that exact scope.

## Escalation Rules

Escalate to the user only for:

1. durable/valuable artifacts found in temp or non-canonical paths;
2. sensitive/high-risk artifacts: credentials, tokens, contracts, health/personal data, private IDs;
3. unlabeled review/audit residue that cannot be safely classified;
4. routing architecture decisions that cannot be auto-resolved;
5. runtime-critical drift, such as a service, symlink, wrapper, or active process pointing at system temp.

Do not escalate ordinary scratch/log/cache residue or clearly reproducible leftovers as a decision.

## Safe Cleanup Defaults

- Use `trash` or a recoverable cleanup mechanism when available; avoid irreversible `rm` for user data.
- Do not delete durable or unclear files without exact approval.
- For low-value scratch/reproducible residue, summarize counts/types rather than asking the user to decide on each file.
- If deleting/moving is required, follow `destructive-operations.md`: exact path/scope, reason, what is not touched, and rollback/safety plan.

## Report Shape

Use a concise report:

```text
File Janitor Audit — <date/scope>

High / needs review:
- <path> — class, why it matters, recommended routing/action

Low / info:
- <path> — false-positive, duplicate, superseded, reproducible, or review-staged context

Auto-cleanup / no decision needed:
- class summary and examples, not a giant dump

Needs user review:
- exact decisions required
```

## Scheduled Janitor Pattern

A nightly Hermes cron job should run this mode for workspaces where residue accumulates. The job is part of the tidy system: it should clean up obvious safe residue automatically, produce a concise durable report, and ask the user only for decisions that require escalation. If the user explicitly asks to operationalize Tidy Hermes or says the janitor cron should exist, create or update the cron job now; do not merely document that a cron would be useful.

For recurring janitor jobs:

- run on a nightly cadence unless the user chooses another schedule;
- prefer a quiet middle-of-the-night slot, at least 30 minutes away from other recurring crons;
- keep the prompt stable and point it at one policy index/reference;
- pin the exact scan scope in the job prompt or referenced policy file;
- auto-tidy only clearly safe `scratch`, stale `reproducible`, and expired `review-staged` residue inside approved cleanup scope;
- do not delete, move, or route `durable`, sensitive, or `unlabeled` artifacts without exact user approval;
- write one durable report path, overwriting or appending according to the user's workflow;
- send the user an escalation prompt when decisions are needed, with exact paths/types/reasons/recommended actions;
- stay silent or send only a terse summary when no escalations are needed;
- keep Docker/image/runtime storage hygiene separate unless the workspace policy explicitly includes it.

Escalation prompt shape:

```text
Nightly File Janitor needs decisions — <workspace/date>

Recommended auto-cleaned:
- <class/count only; no giant dump>

Needs your decision:
1. <path> — class: <durable|sensitive|unlabeled|runtime-critical>; why escalated; recommended action
2. <path> — class: ...

Reply with approvals by number, alternate routes, or "skip".
```

## Verification

Before calling the audit complete:

- policy source and scan scope were pinned;
- findings were classified before escalation;
- sensitive/private findings were not dumped into chat;
- cleanup actions, if any, used approved exact scope;
- durable items have a recommended canonical route;
- false positives and reproducible leftovers were downgraded rather than escalated as noise.
