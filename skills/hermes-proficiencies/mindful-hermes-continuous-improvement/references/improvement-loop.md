# Hermes Improvement Loop

## Purpose

Adapt a mature continuous-improvement loop to Hermes without recreating process that Hermes already handles natively.

## Loop 1: Real-Time Improvement Capture

Trigger when the user corrects Hermes, Hermes catches its own mistake, a recurring behavior failure appears, or a tool failure reveals a reusable gotcha.

Procedure:

1. Identify root cause, not just symptom.
2. Classify as:
   - regression / behavior gap;
   - tool gotcha;
   - capability gap;
   - no durable lesson.
3. Patch the governing skill if the fix is reusable and clear.
4. Save memory only for durable user/environment facts, not task progress.
5. If a durable local log is useful, add a concise entry under the continuous-improvement root.
6. Verify the behavior or workspace state before claiming it is fixed.

Rule: logging without a behavior change is journaling.

## Loop 2: Capability Gap Tracking

Trigger when the user asks for something Hermes cannot do yet, or a missing capability repeatedly blocks execution.

Track only gaps that are likely to recur. Include:

```text
Gap:
Why it matters:
Current blocker:
Likely fix path:
Status:
```

Do not turn every unavailable API, temporary auth issue, or one-off site breakage into a capability gap.

## Loop 3: Daily/Nightly Automated Loops

Hermes-native scheduled loops should use `cronjob`, not ad hoc reminders.

Scheduling rule: recurring improvement crons should not cluster unless they are intentionally chained. Prefer quiet middle-of-the-night slots and keep at least 30 minutes between unrelated recurring jobs. For the local setup, the file janitor belongs around 3:00 AM local time rather than near evening/closeout activity.

Current high-value loops:

- Decision Miner — mines previous day's conversations into pending human-language decisions.
- Tidy File Janitor — audits file/temp/workspace residue and escalates only meaningful findings.
- Weekly Review Card — summarizes trends from continuous-improvement artifacts.

Keep daily output exception-style. If there is nothing important, a one-line “no decisions/no escalations” is enough.

## Loop 4: Weekly Review

Weekly review answers:

- Are regressions decreasing?
- Are repeat patterns showing failed fixes?
- Did crons run?
- Are file-janitor and decision-miner queues being reviewed?
- Did any correction become a skill/memory/tool change?
- Are capability gaps blocking the user's high-leverage work?

## Loop 5: Promotion and Pruning

Promote learnings to always-loaded guidance only when they are proven:

- recurred 3+ times or came from a strong user correction;
- applies across 2+ contexts or is high-impact enough to matter immediately;
- has a concrete mechanical fix;
- is short enough not to bloat boot context.

Prefer patching a specific governing skill over adding broad memory.

## What Hermes Already Does Well

Do not duplicate these with manual docs unless inspection is missing:

- session history → `session_search`;
- reusable procedures → skills;
- durable user preferences → memory;
- scheduled runs → cron;
- skill lifecycle → curator;
- active task state → todo/session state.

The continuous-improvement layer exists to connect these into inspected behavior change.
