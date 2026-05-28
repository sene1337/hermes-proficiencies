# 1-3-1 Framework

## Purpose

Structure any non-trivial decision so the decision-maker gets:

```text
1 clear problem
3 real options with tradeoffs
1 recommendation
```

Use 1-3-1 before asking the user for non-trivial direction. If the answer becomes obvious and is inside Hermes's autonomy boundary, act instead of asking.

## Procedure

### 1. Name the problem in one sentence

Name the fork in the road, not the background.

Bad:

```text
We've been thinking about many ways to handle this and there are many files and tools...
```

Good:

```text
How should we make this decision record survive compaction?
```

If the problem cannot fit in one sentence, split it into multiple decisions.

### 2. Generate three real options

Each option must be genuinely viable. A reasonable person must be able to argue for it.

Real options:

- have different tradeoffs, not just different effort levels;
- are not strawmen designed to make the recommendation obvious;
- may include "do nothing" only when inaction has a real case.

For each option, include:

- what it is;
- key upside;
- key downside;
- cost/effort when relevant.

### 3. Pick one and say why

The recommendation is mandatory. One paragraph max. Tie it to a tradeoff.

Good:

```text
Rec: Option B because speed matters more than completeness here, and we can patch the missing edge cases after the first real use.
```

Bad:

```text
What do you think?
```

## Hidden purpose

The point is not always to present a 1-3-1. The point is to force complete thinking before interrupting the user.

If the 1-3-1 reveals an obvious answer inside the autonomy boundary, decide and move.

## Quick format

```text
Problem: <one sentence>
A: <option> — <tradeoff>
B: <option> — <tradeoff>
C: <option> — <tradeoff>
Rec: <option> because <why>
```

## Quality check

- [ ] Problem is one sentence.
- [ ] Options are genuinely viable.
- [ ] Options differ by tradeoff.
- [ ] Recommendation exists.
- [ ] Recommendation explains why.
- [ ] If a decision is made, outcome is logged or queued for logging.
