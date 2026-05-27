# Agent-Skill-Native Guidance Notes

## Origin

Created on 2026-05-27 when the owner split the old `disciplined-hermes-playbook-sop-standard` into:

- `helpful-hermes-human-playbook-sop-creator` — human-facing Playbooks/SOPs.
- `methodical-hermes-skill-tool-builder` — agent-native skills and Tool SOPs.

## Anthropic Agent Skills / Claude Code Skills — distilled

- Skills are organized folders containing `SKILL.md` plus optional `references/`, `templates/`, `scripts/`, and assets.
- Progressive disclosure is central:
  - Level 1: `name` and `description` are preloaded and drive invocation.
  - Level 2: `SKILL.md` is loaded only when selected.
  - Level 3+: linked files/scripts/resources are loaded only when needed.
- Keep `SKILL.md` lean; move rare, detailed, bulky, or mutually exclusive material into support files.
- Create a skill when the same instruction/checklist/procedure keeps being pasted, or when a project instruction file has become a procedure.
- Start with evaluation: observe concrete agent failures or repeated tasks, then build skills incrementally.
- Watch real skill use for over-triggering, under-triggering, bad trajectories, overreliance, and missing context.
- Scripts/resources are first-class. Use deterministic scripts for repeatable operations when that reduces ambiguity.
- Make clear whether code blocks are reference examples or executable commands/scripts.

## OpenAI GPT-5 / Agents guidance — distilled

- Agent instructions should reduce ambiguity and map steps to specific actions or outputs.
- Define safe vs unsafe actions, stop conditions, escalation thresholds, and handoff rules.
- Calibrate agentic eagerness: specify when to continue autonomously, when to ask, and when to stop.
- Capture branches and edge cases explicitly.
- Apply layered guardrails by action risk: read-only/write, reversible/irreversible, credential/privacy exposure, financial/legal/safety/public impact.
- Tool definitions and procedures should be standardized, tested, reusable, and clearly documented.
- Use evals and iteration rather than assuming a polished document will produce correct agent behavior.

## Design Correction

A human-facing Playbook/SOP asks:

> Can a human understand and execute this artifact?

An agent-native skill asks:

> Will Hermes route, load, act, stop, verify, and update correctly at runtime?

Therefore, agent skills and Tool SOPs need explicit runtime layers covering:

- invocation contract;
- progressive disclosure map;
- action/tool permissions;
- side-effect and risk class;
- stop/ask/escalate rules;
- expected outputs and verification;
- eval cases: should-trigger, should-not-trigger, missing-context, dangerous-action, tool-unavailable, successful-completion;
- post-use invocation/trajectory audit.

## Practical Review Bias

When reviewing agent skills, be especially adversarial about:

- vague `description` fields;
- broad names that collide with neighboring skills;
- missing counter-triggers;
- missing tool permission boundaries;
- hidden destructive/public/credential-bearing side effects;
- no explicit stop/ask/escalate rules;
- large `SKILL.md` files that should be split;
- code blocks that do not say whether they are executable or illustrative;
- skills that look good as docs but do not change agent behavior safely.
