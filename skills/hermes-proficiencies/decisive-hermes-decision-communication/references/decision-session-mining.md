# Decision Session Mining

## Purpose

Recover decisions made in conversation that were not logged in real time, especially decisions the human may forget the rationale for after a few days or a week.

This is a quality standard for identifying decision-shaped moments. The recurring cron/process ownership belongs to `mindful-hermes-continuous-improvement`; this file defines what counts as a decision and how pending entries should read.

Use this as a review/mining pattern, not as an excuse to skip real-time decision tracking.

## Automation status

Hermes may have the ingredients for decision mining — session search, cron jobs, skills, memory, and file tools — but that does not mean a decision miner is already running.

When the user asks whether Hermes already does decision mining, distinguish clearly:

```text
Capability: Hermes can mine sessions when asked.
Operating loop: Hermes only mines automatically if a cron/job/workflow has been configured.
Output policy: mined decisions should start as a pending review queue, not final logged decisions.
```

If tools are available, check configured cron/jobs before answering. If tools are constrained, say the answer is based on visible context only.

For recurring nightly setup, load `mindful-hermes-continuous-improvement` and follow `references/decision-miner-loop.md` there.

## Inputs

Use available sources appropriate to the environment:

- today's session transcript or session search;
- daily log if one exists;
- git history for decision-shaped commit messages;
- existing decision ledger to dedupe;
- project docs where decisions may have landed.

## Detection signals

Decision-shaped language:

- "we decided"
- "let's go with"
- "approved"
- "rejected"
- "the move is"
- "we're doing X"
- a 1-3-1 recommendation accepted by the user

## Classification

Log:

- explicit choices;
- accepted recommendations;
- choices where alternatives were rejected;
- durable behavioral or architecture decisions.

Skip:

- discussions with no conclusion;
- continuations of previous work;
- routine execution;
- file moves and formatting;
- rejected proposals.

## Pending-review format

When mining decisions for review, do not write them as final unless approved. Present a queue:

```markdown
# Pending Decisions — YYYY-MM-DD

1. <short title>
   <2-3 sentences: what was decided, what alternative was rejected, why this choice was made.>
   -> approve/reject?

2. <short title>
   <context>
   -> approve/reject?
```

## Quality bar

Each proposed entry must be understandable by someone who was not in the session, including the future user who remembers the decision but not the rationale. One-line summaries that read like git commits are not enough for review.

## Failure modes

- Mining discussions as decisions: require evidence of explicit choice.
- Too many proposals: raise the bar to non-trivial decisions.
- Missing context: add what alternative was rejected and why.
- Pre-judging outcomes: present approve/reject queue only.
