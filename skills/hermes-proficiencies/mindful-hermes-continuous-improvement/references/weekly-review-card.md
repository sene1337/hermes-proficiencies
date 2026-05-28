# Weekly Review Card

## Purpose

Give the user a short inspection surface for the improvement system.

The weekly card is not a giant report. It answers whether Hermes is actually improving or just accumulating logs.

## Shape

```text
SELF-IMPROVEMENT WEEKLY CARD

Regressions:      <new count + repeat patterns>
Wins:             <specific wins tied to prior failures>
User corrections: <count / trend>
Capability gaps:  <opened / closed / blocking>
Decision queue:   <pending count / needs review?>
Janitor:          <escalations / clean?>
Cron health:      <failures / ok>
Trend:            <improving / flat / slipping>

One recommendation:
<what to change this week>
```

## Inspection Questions

- Are regressions getting less frequent?
- Are repeats showing that a fix failed?
- Are wins tied to real prior failures?
- Are decision-miner entries being reviewed?
- Are janitor findings meaningful or noisy?
- Did all crons run?
- Are capability gaps blocking the user's high-leverage work?

## Escalation Thresholds

- Same pattern 3+ times → current fix failed; propose a different mechanism.
- Cron failures 2+ days → monitoring gap; fix the cron.
- Pending decision queue grows without review → surface it more directly.
- Janitor repeatedly finds durable residue → strengthen file routing or workspace hygiene.
- User corrections increase → patch governing skills and simplify process.
