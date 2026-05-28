# Playbook / SOP / Tool SOP / Skill Artifact Map

Use this reference when a session is about converting user-built playbooks, SOPs, review protocols, or tool procedures into Hermes skills without flattening them into one generic documentation artifact.

## Core distinction

All four artifact types are **skill-shaped**: they encode repeatable behavior, triggers, procedures, quality checks, and improvement loops.

They differ by primary operator and runtime consequence:

```text
Human Playbook
  Operator: human / organization
  Purpose: doctrine, operating model, cadence, principles, accountability
  Governing skill: helpful-hermes-human-playbook-sop-creator
  Score against: Human Playbook Standard

Human SOP
  Operator: human
  Purpose: exact repeatable steps for a known human task
  Governing skill: helpful-hermes-human-playbook-sop-creator
  Score against: Standard Human SOP Standard

Tool SOP Skill
  Operator: Hermes / agent runtime
  Purpose: safe use of a CLI, API, repo, browser flow, platform, MCP server, vault, or local workflow
  Governing skill: methodical-hermes-skill-tool-builder
  Score against: Tool SOP Skill Standard

Agent Skill / Proficiency
  Operator: Hermes / agent runtime
  Purpose: reusable behavior, judgment, routing, guardrails, evals, and verification across a class of tasks
  Governing skill: methodical-hermes-skill-tool-builder
  Score against: Agent Skill Standard

Review Protocol
  Operator: human, agent, or both depending on target
  Purpose: scoring/control loop for an artifact type
  Governing skill: attach to the artifact type being scored; use both human and agent standards when the target crosses the boundary
  Score against: the target artifact standard + locked-evaluator rule
```

## Routing rule

Do not decide by the source artifact's label alone. Decide by what the finished artifact must make possible.

```text
If the output helps a human understand, decide, inspect, or execute:
  route to helpful-hermes-human-playbook-sop-creator.

If the output changes how Hermes loads context, calls tools, writes files, handles risk, verifies work, or remembers reusable procedure:
  route to methodical-hermes-skill-tool-builder.

If the output does both:
  split the artifact or create a pair:
    - human-facing playbook/SOP for doctrine and human operation;
    - Hermes skill/Tool SOP for agent execution.
  Cross-link them, but do not blend human UX prose and runtime guardrails into one overloaded standard.
```

## Meta-skill pattern

When the user asks for “a skill that teaches Hermes how to create playbook skills, SOP skills, Tool SOP skills, and score them,” treat it as a **reusable meta-skill** problem:

1. Classify the artifact family first: human-facing, agent-runtime, tool-runtime, review/scoring, or mixed.
2. Keep the reusable standard in a rich `SKILL.md`.
3. Put session-specific source comparisons, imported source examples, score sheets, and taxonomy notes in `references/`.
4. Put copyable artifact starters in `templates/`.
5. Put deterministic validators/scorers in `scripts/` only when the process becomes exact and repeated.
6. Avoid one-session-one-skill proliferation; add modes/support files under the relevant umbrella.

## source import taxonomy watchlist

During future imports, classify each artifact by domain of operation before choosing a runtime category. Avoid vague final buckets like `documentation`, `operations`, or `software-development` when the artifact's actual domain is narrower.

Keep these as pending governance questions until enough imports are visible:

- Which source playbooks become human-facing Hermes proficiencies vs private local Tool SOP skills?
- Which artifacts should remain human docs rather than skills?
- Which Tool SOPs are private/local because they depend on the user's accounts, vaults, local machines, iCloud paths, or credentials?
- Which proficiencies are public/shareable after privacy and portability review?
- Which review protocols belong inside parent skills vs standalone root standards?

## Scoring shortcut

Before scoring, pin:

- exact artifact path/source/version;
- intended operator;
- standard used;
- whether the artifact is current runtime, private source, public candidate, historical, or pasted draft.

If operator and standard do not match, stop and re-route before scoring. A human SOP can look excellent as documentation while failing as an agent skill; a Tool SOP can be safe for Hermes while being too terse for a human operator.
