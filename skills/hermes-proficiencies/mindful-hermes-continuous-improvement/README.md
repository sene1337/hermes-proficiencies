# Mindful Hermes Continuous Improvement

This skill gives Hermes a practical improvement loop.

The goal is not to make the agent write more logs. The goal is changed behavior. A useful loop looks like this:

```text
mistake -> root cause -> fix -> verify it stuck
```

If Hermes only records the mistake, that is journaling. If it fixes something once and never checks whether the fix held, that is hoping. This skill keeps the improvement system honest.

It owns the recurring feedback loops around the agent:

- catching regressions and patching the governing skill;
- tracking capability gaps that keep blocking work;
- mining conversations for decisions the user may forget later;
- reviewing file-janitor findings without turning the user into a filesystem janitor;
- producing a compact weekly card that shows whether the agent is improving or just accumulating process.

The skill is intentionally Hermes-native. It does not recreate session history, memory, skills, cron, or curator as manual documents. It uses those primitives and adds inspection so they produce better behavior.

Use this when a correction should change future behavior, when a recurring cron/report needs ownership, or when a process starts feeling like paperwork instead of progress.
