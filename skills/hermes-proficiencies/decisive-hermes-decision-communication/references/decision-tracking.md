# Decision Tracking

## Purpose

Capture strategic, behavioral, architectural, and workflow decisions with enough reasoning that they survive human forgetfulness, compaction, and future context loss.

The primary customer is often the future human: in a week the user may ask, "why did we decide that?" The log should make the answer obvious so work keeps moving fast without relitigating the decision.

## When to log

Log when the user:

- sets or changes strategic direction;
- makes a behavioral decision about how we work;
- chooses architecture, tool structure, or process structure;
- makes a call future-us would ask "why did we do it this way?";
- makes a call the user is likely to forget the rationale for within days or weeks;
- explicitly says a decision should be preserved so future momentum is not lost;
- approves/rejects a 1-3-1 recommendation.

Do not log:

- routine execution;
- housekeeping, file moves, or formatting;
- project-level tactical details that belong in project docs;
- reversals of mistakes;
- discussions without a decision.

## Minimum entry

```text
YYYY-MM-DD | what was decided | why, one line
```

The entry must answer:

1. What was decided?
2. Why? What problem does it solve or what alternative was rejected?
3. What should future-us remember so the decision does not get reopened unnecessarily?

## Procedure

1. Capture the decision in one line.
2. Capture the why in one line.
3. If the workspace has an approved decision ledger, append immediately.
4. If the ledger path is not approved or available, queue the entry in the final response or task notes for user approval.

## Quality examples

Weak:

```text
2026-05-28 | Use 1Password PAT | GitHub
```

Better:

```text
2026-05-28 | GitHub writes use 1Password-backed agent credentials, not ambient keychain auth | Prevents accidental pushes with the wrong account and keeps auth source explicit.
```

## Relationship to session mining

Real-time tracking is primary. Session mining is a safety net for decisions missed during the conversation.
