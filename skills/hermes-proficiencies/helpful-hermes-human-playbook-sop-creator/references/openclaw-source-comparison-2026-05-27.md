# OpenClaw Source Comparison — 2026-05-27

## Context

the owner asked whether Grok stripped too much from the original OpenClaw Playbook Creation / SOP Creation / Review Protocol materials when converting them into `helpful-hermes-human-playbook-sop-creator`.

Original source documents reviewed:

- `~/.openclaw/workspace/ops/playbooks/playbook-creation/playbook-creation.md`
- `~/.openclaw/workspace/ops/playbooks/playbook-creation/sops/sop-creation.md`
- `~/.openclaw/workspace/ops/playbooks/playbook-creation/sops/sop-templates.md`
- `~/.openclaw/workspace/ops/playbooks/playbook-creation/sops/review-protocol.md`

## Finding

The Hermes skill preserved the broad structure, but the first conversion softened several operationally important rules. The skill should remain Hermes-native and human-facing, but regain OpenClaw's sharper accountability and execution discipline.

## High-value OpenClaw details to preserve

- Owner / Reviewer / Review Cadence should be first-class fields, not buried in prose.
- Playbooks should be copy-paste executable: if the operator cannot directly follow a checklist, template, script, framework, or artifact, the playbook is too theoretical.
- Principles can be marked `TBD — refine after first 3 executions` for v1.0 when the domain is still forming. Do not invent fake principles to look complete.
- SOP source methods matter:
  - Capture Method — document what already works but keeps getting forgotten.
  - Interview Method — extract the process from someone who knows how.
  - Camcorder / Black Box Method — do it once, record every step, then extract the SOP.
- Explore before writing. Do not infer from names. An “inbox” might be email, files, a database, or a physical tray.
- Use the defined sections by default. If an extra section is needed, flag it for review and explain why the template should evolve.
- Name for the general case. Pressure-test: would this name still work if the tool changed, the team doubled, or the use case expanded?
- Changelog is append-only. Do not rewrite operational history.
- Lightweight SOPs need full polish + adversarial review within 7 days if they remain useful.
- Important review score sheets should be saved or durably summarized; do not rely on chat history.
- If reviewer misses two consecutive reviews, owner escalates or marks the artifact provisional/abandoned.
- Keep a quick self-check before the heavier adversarial scoring protocol.

## Design decision

Do not revert to raw OpenClaw docs. Keep the Hermes skill improvements:

- human-facing scope;
- separation from agent/tool runtime standards;
- artifact type decision tree;
- version pinning;
- audience/operator clarity;
- stronger scoring rubric.

Patch the skill by adding OpenClaw's operational teeth back into the Hermes-native structure.
