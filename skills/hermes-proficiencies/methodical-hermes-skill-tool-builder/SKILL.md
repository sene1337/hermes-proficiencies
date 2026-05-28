---
name: methodical-hermes-skill-tool-builder
description: Use when creating, converting, or reviewing Hermes agent skills, Tool SOPs, or agent-runtime skill procedures. Guides Hermes to build reliable skills with invocation contracts, progressive disclosure, tool boundaries, guardrails, evals, and verification.
version: 1.2.5
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [proficiency, methodical, agent-skills, tool-sops, runtime, evals, guardrails]
    related_skills: [hermes-agent-skill-authoring, tidy-hermes-workspace-hygiene, thorough-hermes-skill-publishing, helpful-hermes-human-playbook-sop-creator]
---

# Methodical Hermes Skill/Tool Builder

## Overview

Install the **methodical builder** proficiency: Hermes turns repeated agent behaviors, tools, workflows, review standards, and Tool SOPs into reliable runtime skills.

This skill is for agent-native artifacts. It should help Hermes route, load, act, stop, verify, and improve correctly without dragging every rubric, template, and historical note into the default context.

Use the main file as the router. Load support files only when the task needs them.

## When to Use

Use this skill when:

- The user asks to create, fork, rewrite, slim, harden, or review a Hermes skill.
- The artifact should teach Hermes reusable behavior rather than only produce a human document.
- The artifact is a Tool SOP for a CLI, API, repo, browser workflow, MCP server, platform, account, or Hermes tool.
- A workflow needs tool permissions, side-effect boundaries, stop/ask/escalate rules, validation, scripts, or structured outputs.
- A skill, Tool SOP, Review Protocol, or lightweight draft needs scoring or tightening.
- A human playbook/SOP is becoming agent-executable and needs to graduate into skill form.

Do not use this for:

- Purely human-facing playbooks/SOPs; use `helpful-hermes-human-playbook-sop-creator`.
- Public publishing checks by themselves; use `thorough-hermes-skill-publishing`.
- File routing/workspace cleanup by itself; use `tidy-hermes-workspace-hygiene`.
- Hermes syntax/frontmatter mechanics alone; use `hermes-agent-skill-authoring`.
- One-off answers that do not create durable agent behavior.

## Neighbor Routing

```text
Human-facing playbook / SOP / operating doc
→ helpful-hermes-human-playbook-sop-creator

Agent-runtime skill / Tool SOP / skill scoring / reusable agent behavior
→ methodical-hermes-skill-tool-builder

Agent is about to create/edit/move/delete files, route artifacts, touch git/source/runtime, or do workspace operations
→ tidy-hermes-workspace-hygiene

Publish/share/export/GitHub/release a skill
→ thorough-hermes-skill-publishing
```

Load neighboring skills only when their domain changes the action. Do not load every neighbor just because it is related.

Exception: `tidy-hermes-workspace-hygiene` is not only user-request-triggered. Load it whenever Hermes itself is about to create, edit, move, delete, sync, publish, or leave durable files behind. Its purpose is to prevent agent-made workspace messes.

## Runtime Contract

Hermes may autonomously:

- classify artifact type and complexity tier;
- draft or review skill content in chat;
- read relevant skill files and support files in the approved workspace;
- create or patch the user's tracked private runtime skills when edit scope is clear;
- propose score sheets, eval cases, support-file maps, and verification plans.

Hermes must ask before:

- deleting, moving, replacing, or bulk-syncing skill directories/files;
- publishing, pushing, or changing public/shared repos;
- editing protected wiki/knowledge-base paths;
- choosing a new taxonomy/source placement when that is a governance decision;
- making high-impact/destructive changes outside the approved scope.

Stop immediately when:

- the artifact type or source of truth is unclear and guessing would change file actions;
- a public export might include private/local material;
- a destructive approval is denied;
- a protected path is in scope without exact write approval.

Expected final evidence for edit tasks:

- files changed;
- source/runtime relationship;
- validation or deferred validation;
- git status/commit when applicable;
- any support files, evals, or governance decisions deferred.

## Artifact Type Decision

Pick the artifact type before writing.

```text
Reusable agent behavior across a domain
→ Agent Skill

Tool/API/CLI/repo/browser/MCP/platform/account workflow
→ Tool SOP Skill

Scoring/review/control loop for skills, tools, or agent procedures
→ Review Protocol inside the relevant skill or as a dedicated skill

Human-facing playbook or SOP with no agent-runtime behavior
→ helpful-hermes-human-playbook-sop-creator

Early low-risk experiment
→ Lightweight Skill Draft, explicitly provisional
```

Do not collapse these into generic documentation. The common shape is repeatable operating knowledge; the deciding factor is the primary operator and runtime consequence.

## Complexity Tiers

Choose the lowest sufficient tier.

```text
Tier 0 — Simple instruction / tiny Tool SOP
  Low-risk repeated tool/use pattern. Needs trigger, do/don't, one or two executable patterns, verification/gotchas. No heavy rubric or multi-file structure unless clearly useful.

Tier 1 — Normal Agent Skill or Tool SOP
  Reusable behavior with meaningful ambiguity, side effects, or recurring failure modes. Needs lean SKILL.md, practical procedure, key runtime boundaries, and compact eval/observed-use notes.

Tier 2 — High-risk / multi-mode / public-facing skill
  Publishing, credentials, protected paths, destructive actions, external posting, expensive operations, or several distinct modes. Needs mode router, support files, stronger guardrails, and real validation.
```

Default to the smallest structure that would prevent the observed failure.

## Creation / Edit Procedure

1. **Pin scope and source.** Identify artifact, path/source, runtime/private/public status, and whether editing is authorized.
2. **Classify artifact type.** Agent Skill, Tool SOP, Review Protocol, human Playbook/SOP redirect, or Lightweight Draft.
3. **Choose tier.** Do not force progressive disclosure, gradient design, full scoring, or support files onto Tier 0 work.
4. **Survey neighbors.** Check existing skill names/descriptions enough to avoid trigger collision.
5. **Draft metadata first.** Name and description are routing surfaces. Make the description start with a concrete `Use when...` trigger.
6. **Keep `SKILL.md` lean.** Put only default-path behavior in the main file. Move bulky, rare, historical, templated, deterministic, or risk-specific material into support files.
7. **Set action boundaries.** Name autonomous actions, approval-required actions, stop conditions, expected outputs, and verification.
8. **Add support files only when useful.** Choose `references/`, `templates/`, `scripts/`, or `assets/` by purpose. Add a one-line pointer in `SKILL.md`.
9. **Review proportional to risk.** Use quick self-check for Tier 0. Use the full review protocol for important, disputed, high-risk, or public-bound skills.
10. **Verify and commit.** For tracked private runtime skills, inspect diff and commit durable changes. For public-bound skills, run the publishing workflow separately.
11. **Observe and patch.** If real use shows wrong invocation, unsafe action, or missing guidance, patch the governing skill rather than treating it as a one-off.

## Playbook/SOP Translation Pattern

Preserve the original operating architecture instead of collapsing every source artifact into one heavyweight skill.

```text
Playbook layer
  Broad posture, principles, routing signals, and "don't make a mess" guidance.
  In Hermes: usually the main SKILL.md or compact skill wrapper.

SOP layer
  Exact procedures for a specific situation.
  In Hermes: focused support files under references/, templates/, or scripts/.

Tool SOP layer
  Tool/API/CLI/platform do/don't/verify instructions.
  In Hermes: often Tier 0; do not force full Playbook/SOP machinery.
```

Good progressive disclosure preserves this separation:

```text
Skill / Playbook = posture + mode signals
Focused SOPs = exact procedures
Tool SOPs = minimal executable do/don't/verify instructions
```

## Minimum Agent Skill Shape

For normal Agent Skills, use `templates/agent-skill.md` when drafting. Minimum runtime quality bar:

- specific name and `Use when...` description;
- clear trigger and counter-trigger;
- objective/success condition;
- runtime contract with tool/action boundaries;
- practical operating procedure;
- support-file map if support files exist;
- verification and eval/observed-use notes proportional to risk;
- practical pitfalls/gotchas.

## Minimum Tool SOP Shape

For Tool SOPs, use `templates/tool-sop.md` when drafting. Minimum runtime quality bar:

- 10-second quick ref when useful;
- when this tool beats alternatives and when not to use it;
- exact executable usage patterns;
- safe defaults and approval thresholds;
- credential/privacy/public/destructive/cost guardrails;
- verification/health checks;
- gotchas from real or plausible failures.

Tier 0 Tool SOPs can be short. They only need the trigger, do/don't rules, one or two executable patterns, verification, and gotchas.

## Review Procedure

Use the full review protocol only when the user asks for scoring/review, the skill is high-risk, the result is disputed, or public/shared release is near.

Short review loop:

1. Pin exact artifact version/source.
2. Choose standard: Agent Skill, Tool SOP, Review Protocol, human redirect, or publishing readiness.
3. Check trigger/frontmatter collision, runtime boundaries, executability, safety, verification, portability, and maintainability.
4. Quote exact gaps when edits are needed.
5. Fix gaps.
6. Re-score only if a numeric score/readiness claim is being made.

Detailed rubric, score bands, locked-evaluator rule, score sheet, and parent-feedback procedure live in `references/review-protocol.md` and `templates/score-sheet.md`.

## Skill Library Update / Curation

When the user asks to update the skill library after a session, be active by default.

- Prefer patching a loaded or governing reusable skill before creating a new narrow skill.
- Treat user corrections about style, format, verbosity, workflow, sequencing, or tool boundaries as strong skill signals. Patch the governing skill body so the next session starts with the corrected behavior; memory alone is not enough.
- Capture reusable procedure/pitfall, not session narrative or transient task progress.
- If the user says the session was poisoned, compacted, or context was lost, stop extending the trajectory until the exact active step/scope is recovered. If recovery is not confident, ask before editing files, committing, publishing, deleting, or marking work complete.
- Obey explicit tool constraints literally. Do not call denied tool types and do not claim git/diff/source-runtime validation unless actually checked or visible in context.
- When the user restricts a skill-library update pass to memory and skill-management tools, treat that as excluding unrelated planning, search, shell, file, git, validation, and todo tools. Use visible conversation context plus loaded skill content; patch through `skill_manage`; report validation/git evidence as deferred or already visible only if it is actually visible.
- Under a constrained curation surface, still make narrow useful skill patches through allowed tools rather than stalling on unavailable verification.
- If nothing genuinely reusable emerged, say `Nothing to save.`

## Public / GitHub Publishing Boundary

For public/shared publishing, stop and load `thorough-hermes-skill-publishing`.

Internal skill changelogs are package-local maintenance notes for the user and for users who install/maintain the skill locally. They are not the public GitHub changelog.

Public exports should remove:

- `## Changelog` sections from runtime files;
- internal changelog pointers;
- private paths, personal names, chat IDs, repo names, local-only policy, and source-system attribution.

Public changelog content belongs in GitHub release notes, PR summaries, repo changelogs, or another public-facing summary.

## Progressive Disclosure

Support files for this skill:

- `references/review-protocol.md` — full scoring rubric, locked-evaluator rule, score bands, and parent-feedback procedure.
- `references/eval-cases.md` — eval cases for this skill and model cases for new skills.
- `references/failure-modes.md` — long failure-mode checklist for deeper reviews.
- `references/support-file-format-guide.md` — support-file formats, mode-router pattern, and gradient design.
- `references/private-skill-taxonomy.md` — private taxonomy, artifact-type/category decision flow, source placement, naming, attribution, and public-export wording hygiene.
- `references/playbook-sop-skill-artifact-map.md` — map across Playbooks, SOPs, Tool SOPs, Review Protocols, and Hermes skills.
- `references/credential-tool-sop-porting-notes.md` — credential/secret-vault Tool SOP porting guardrails.
- `references/agent-skill-native-guidance.md` — source guidance from Agent Skills / Claude Code / GPT-5 / Agents research.
- `templates/agent-skill.md` — copyable Agent Skill starter.
- `templates/tool-sop.md` — copyable Tool SOP starter.
- `templates/score-sheet.md` — copyable score sheet.

Load only the selected support file(s). Do not load every reference by default.

## Common Failure Modes

Top failures to prevent on the default path:

1. **Complexity tier skipped.** Simple Tool SOPs become bloated framework skills. Fix: choose Tier 0/1/2 before writing.
2. **Playbook/SOP layers collapsed.** Posture and exact procedures get mixed into one monolith. Fix: main skill routes; focused SOPs hold procedures.
3. **Everything stuffed into `SKILL.md`.** Fix: move bulky, rare, historical, templated, or risk-specific detail to support files.
4. **Neighboring-skill collision.** Fix: narrow descriptions and counter-triggers.
5. **Tool permissions implicit.** Fix: state autonomous vs approval-required actions.
6. **No stop conditions.** Fix: name ambiguity/risk/tool-failure stop rules.
7. **Post-upgrade score laundering.** Fix: do not claim a new score/readiness band without re-scoring.
8. **Verification overclaim.** Fix: report only evidence actually checked.
9. **Private material in public export.** Fix: run publishing workflow and strip internal changelogs/private context.
10. **Observed failures stay local.** Fix: patch the governing skill.
11. **Passive curation under tool constraints.** Fix: when the user limits the curation pass to memory and skill-management tools, still patch the loaded/reusable skill through `skill_manage`; report deferred git/diff/validation instead of doing nothing or attempting denied tools.
12. **Tool-surface leakage during curation.** Fix: if the prompt says only memory and skill-management tools are allowed, do not call `todo`, `session_search`, shell/git/file validation, or other helper tools even if they would normally improve process discipline. Use visible context and make the smallest safe skill patch.
13. **Post-compaction assumption.** Fix: after compaction/context loss, do not infer missing numbered steps from adjacent topics. Re-anchor from visible context and allowed recovery tools; if exact step/scope is still uncertain, ask the user before any file edit, commit, publish/delete action, or completion claim.

Use `references/failure-modes.md` for the full checklist.

## Verification Checklist

Before calling an Agent Skill or Tool SOP done:

- [ ] Correct artifact type and complexity tier selected.
- [ ] Description starts with a concrete `Use when...` trigger.
- [ ] Trigger and counter-trigger are clear and do not collide with neighboring skills.
- [ ] Runtime contract/action boundaries/stop rules are explicit enough for the tier.
- [ ] `SKILL.md` is lean; support files carry bulky detail.
- [ ] Tool SOPs include exact executable patterns and verification.
- [ ] Public publishing checks are separate and remove internal changelogs/private context.
- [ ] Important/high-risk artifacts were reviewed with `references/review-protocol.md`, or review was explicitly deferred.
- [ ] Any post-patch score/readiness claim is backed by a real re-score or labeled as an estimate.
- [ ] Git/status/diff/commit evidence is included when files were edited.

## Source Lineage

Forked from `disciplined-hermes-playbook-sop-standard` on 2026-05-27 after review against Anthropic Agent Skills / Claude Code Skills and OpenAI GPT-5 / Agents guidance. The original standard was split into a human-facing Playbook/SOP creator and this agent-skill/tool-SOP builder.
