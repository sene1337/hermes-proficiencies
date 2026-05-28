# RICE Scoring

## Purpose

Use RICE to decide what to do first when multiple tasks compete for the same time slot.

1-3-1 chooses an approach. RICE orders competing tasks.

## When to use

Use RICE when:

- multiple tasks are competing for attention;
- the user asks "what is the priority order?";
- prioritization is looping;
- the tradeoff is about sequence, not strategy.

Do not use RICE for:

- one obvious next step;
- choosing an approach;
- high-stakes decisions where qualitative judgment dominates;
- fake precision when inputs are unknown.

## Formula

```text
Score = (Reach x Impact x Confidence) / Ease
```

Factors:

```text
Reach: how many people/files/projects/workflows it affects, 1-10
Impact: how much it moves the needle, 1-10
Confidence: how sure we are, 1-10
Ease: how easy it is, 1-10; higher means easier
```

Higher score means do first.

## Mobile-friendly output

Use stacked bullets, not raw Markdown tables:

```text
1. File routing SOP -> 90
   Reach 10 / Impact 8 / Confidence 9 / Ease 8
   Why: affects every future file operation.

2. Deep trawler fix -> 30
   Reach 5 / Impact 6 / Confidence 8 / Ease 8
   Why: useful but narrower.
```

## Pitfalls

- Do not pretend RICE is objective when scores are guesses.
- Do not use RICE to avoid making a recommendation.
- Do not over-score low-impact busywork because it is easy.
- Do not use raw tables in Telegram.
