---
name: mindful-hermes-continuous-improvement
description: "Use when Hermes needs to maintain the user's continuous-improvement loop: capture regressions, capability gaps, decision-miner outputs, file-janitor findings, cron health, and weekly review cards without turning native Hermes strengths into process theater."
version: 1.0.3
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [proficiency, continuous-improvement, regressions, crons, decision-mining, janitor, review]
    related_skills: [tidy-hermes-workspace-hygiene, decisive-hermes-decision-communication, methodical-hermes-skill-tool-builder, user-context-loading]
---

# Mindful Hermes Continuous Improvement

## Overview

Install the continuous-improvement loop for Hermes.

This skill is not about making more docs. It is about making the agent get better in visible, inspected ways:

```text
mistake → root cause → fix → verify it stuck
```

The loop is the capability. Logging without fixing is journaling. Fixing without verification is hoping.

This skill ports the useful parts of a mature continuous-improvement process into Hermes while avoiding duplication of things Hermes already does well naturally: skills, memory, session search, cron jobs, curator, and normal tool verification.

## When to Use

Use this skill when:

- The user corrects Hermes and the correction points to a repeatable behavior gap.
- Hermes makes or catches a mistake that should change future behavior.
- A missing capability blocks the user's work repeatedly.
- A nightly/weekly improvement loop needs to run, be checked, or be created.
- Decision-miner, file-janitor, or weekly-review-card outputs need review.
- A process is turning into logging theater instead of changed behavior.
- The user asks to port or maintain a mature continuous-improvement process in Hermes.

Do not use this skill for:

- One-off tool errors with no reusable lesson.
- Routine task status updates.
- Creating a narrow skill when patching an existing governing skill would fix the behavior.
- Replacing Hermes native memory/skills/session search/curator with duplicate manual docs.

## Runtime Contract

Hermes may autonomously:

- classify a correction as regression, capability gap, decision candidate, janitor finding, or no-log-needed;
- patch the governing Hermes skill when the reusable fix is clear;
- create or update pending review files inside an approved local continuous-improvement workspace;
- create or update non-destructive cron jobs that the user explicitly requested;
- prepare concise weekly review cards from existing artifacts;
- report cron health and improvement-loop status.

Hermes must ask before:

- writing to protected knowledge bases;
- creating noisy daily reports that will burden the user;
- deleting, archiving, or bulk-rewriting historical improvement files;
- promoting a learning into always-loaded memory/boot context when it is not proven;
- auto-moving pending decisions into the permanent decision ledger without explicit approval.

Stop when:

- the proposed loop duplicates a native Hermes feature without adding inspection or behavior change;
- the source of truth for a ledger/report path is unclear and writing would create drift;
- a logged regression has no root-cause or no concrete fix;
- the same pattern appears 3+ times and the current fix is obviously not working.

## Core Principles

1. **The loop is the capability.** Capture, fix, verify. Missing any step means the loop failed.
2. **Behavior changes beat more docs.** Patch skills, prompts, crons, or tools. The doc is the receipt, not the cure.
3. **Verify against reality.** Use files, session search, git, cron status, and tool outputs. Do not trust memory alone.
4. **Wins matter too.** Track wins that prove a previous regression is improving.
5. **Inspect what you expect.** A cron or report nobody reviews is not a system.
6. **Stay native to Hermes.** Prefer memory for durable user preferences, skills for reusable procedures, session search for transcript recall, cron for scheduled loops, and curator for skill lifecycle.

## Loop Router

```text
User correction / agent mistake / repeatable behavior failure
→ Real-time improvement capture. Patch the governing skill immediately when clear.

Missing capability blocks work repeatedly
→ Capability gap. Log with blocker and next concrete path.

Decision made in conversation that the future user may forget
→ Decision miner loop. Pending review first, permanent ledger after approval.

Files/temp/workspace residue accumulates
→ Tidy Hermes file-janitor loop.

Recurring loops may be stale or noisy
→ Weekly review card / cron health inspection.

Proven learning recurs across contexts and survives time
→ Promote carefully to skill/memory/boot-level guidance.
```

## Local path policy

Use the user's existing continuous-improvement locations when they exist. Keep the split between pending review queues and permanent ledgers:

```text
Continuous-improvement root:
<continuous-improvement-root>/

Pending decision miner output:
<continuous-improvement-root>/pending-decisions-session-miner.md

Permanent decision ledger:
<decision-ledger-root>/decision-ledger.md

File janitor report:
<continuous-improvement-root>/file-janitor-report.md
```

Do not invent a new destination if the user already has a working one.

## Operating Procedure

1. **Classify the signal.** Regression, capability gap, decision, file residue, cron health, win, or no-log-needed.
2. **Use the native Hermes home.** Memory for durable user facts, skills for behavior, cron for scheduled loops, session search for recall, file reports for review artifacts.
3. **Fix before logging when possible.** If the behavior fix is clear, patch the governing skill now.
4. **Log only what helps future behavior.** Avoid status dumps and developer trivia.
5. **Keep the user's review burden low.** Pending queues should contain decisions, escalations, or exceptions — not raw dumps.
6. **Verify the loop.** Check cron status, file output, skill diffs, or session evidence before claiming improvement.
7. **Escalate repeats.** Same pattern 3+ times means the fix failed; propose a different mechanism.

## Support Files

- `references/improvement-loop.md` — mechanical loops adapted from the source system, with Hermes-native boundaries.
- `references/decision-miner-loop.md` — nightly decision-miner process and pending-vs-final ledger rules.
- `references/weekly-review-card.md` — compact inspection card for the user.

## Eval Cases

### User correction

User says: “Stop reporting dirty git state to me; clean it.”

Expected: classify as behavior regression, patch the governing skill, save user preference if durable, and verify workspace clean. Do not merely apologize.

### Decision made

User says: “We’re going with Option B because it keeps velocity high.”

Expected: if in real-time, offer/queue a human-language decision entry. If in nightly mining, add to pending decisions, not directly to permanent ledger.

### Native Hermes duplicate

Agent proposes a manual daily transcript archive even though session search already stores conversations.

Expected: reject or simplify. Use session search; only add a review loop if it changes behavior or preserves decisions.

### Janitor noise

Nightly file janitor finds ordinary caches and logs.

Expected: auto-classify/ignore safe residue and only escalate durable, sensitive, unlabeled, or runtime-critical findings.

## Common Failure Modes

- **Logging theater:** entries pile up, behavior does not change. Fix: patch skills/tools/crons; verify later.
- **Over-process:** recreating Hermes native memory/session/curator functionality as manual docs. Fix: use native primitives.
- **No inspection:** crons run but the user never sees the meaningful queue/card. Fix: concise review output with only decisions/exceptions.
- **Premature promotion:** noisy lessons added to always-loaded context. Fix: require recurrence, multi-context evidence, and survival over time.
- **Decision auto-finalization:** miner writes straight to permanent ledger. Fix: pending review first unless auto-logging was explicitly approved.
- **Loop ownership drift:** a recurring inspection/mining process gets embedded in the adjacent domain skill instead of this continuous-improvement skill. Fix: keep the operating loop here and load the domain skill only for quality standards, e.g. decision-miner cron owned here while `decisive-hermes-decision-communication` defines what counts as a good decision entry.

