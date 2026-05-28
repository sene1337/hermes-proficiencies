# Decision Miner Loop

## Purpose

Mine the previous day's conversations for decisions that the future user may forget the rationale for, then create a human-review queue.

This loop belongs to continuous improvement because it is an operating feedback loop. It uses `decisive-hermes-decision-communication` for decision quality, but the scheduled mining process is owned here.

## Default Flow

```text
nightly cron → pending human-language entries → the user approves/rejects → permanent decision ledger
```

## Canonical Local Paths

Preserve the existing pending-vs-final split unless the user chooses a new destination:

```text
Pending review queue:
<continuous-improvement-root>/pending-decisions-session-miner.md

Permanent decision ledger:
<decision-ledger-root>/decision-ledger.md
```

## What to Mine

Look for:

- explicit choices: “we decided,” “approved,” “let's go with,” “the move is,” “we're doing X”;
- accepted recommendations;
- rejected alternatives with rationale;
- durable workflow, architecture, strategy, communication, or behavioral calls;
- decisions the user is likely to ask about later: “why did we do it this way?”

Skip:

- routine execution;
- file moves and formatting;
- tool hiccups with no durable decision;
- mistake reversals;
- discussions with no explicit choice;
- rejected proposals that did not become direction.

## Entry Quality Bar

Pending entries must be written for the future user, not as git commits.

Each entry should answer:

1. What did we decide?
2. Why did we decide it?
3. What alternative/tradeoff did we reject?
4. What should future-us remember so we do not reopen it unnecessarily?

## Pending Review Format

```markdown
---

## YYYY-MM-DD

1. **Short decision title** — 2-4 sentences in the user's language explaining what was decided, why, rejected alternative/tradeoff, and what future-us should remember.
   -> approve/reject?
```

If nothing is found:

```markdown
---

## YYYY-MM-DD

No decisions detected.
```

## Cron Prompt Requirements

A nightly decision-miner cron should:

- run after the day ends, usually 1 AM local time;
- mine the previous local-calendar day;
- use session search plus available files/session store as evidence;
- read pending + permanent ledgers enough to dedupe;
- append pending entries only;
- deliver a concise review queue to the user;
- never write final ledger entries unless the user explicitly approved auto-logging.

## Failure Modes

- **No review loop:** pending entries pile up. Fix: include the queue in morning/weekly review.
- **Too many weak entries:** raise the bar to durable decisions only.
- **Developer language:** rewrite for human rationale and future memory.
- **Auto-finalizing:** keep pending-vs-final split unless explicitly changed.
