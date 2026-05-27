---
name: methodical-hermes-skill-tool-builder
description: Use when creating, converting, or reviewing Hermes agent skills, Tool SOPs, or agent-runtime skill procedures. Guides Hermes to build reliable skills with invocation contracts, progressive disclosure, tool boundaries, guardrails, evals, and verification.
version: 1.1.16
author: Hermes Agent (adapted from OpenClaw plus agent-skill guidance)
license: MIT
metadata:
  hermes:
    tags: [proficiency, methodical, agent-skills, tool-sops, runtime, evals, guardrails]
    related_skills: [hermes-agent-skill-authoring, tidy-hermes-workspace-hygiene, thorough-hermes-skill-publishing, helpful-hermes-human-playbook-sop-creator]
---

# Methodical Hermes Skill/Tool Builder

## Overview

Install the **methodical builder** proficiency: Hermes should turn repeated agent behaviors, tools, workflows, and review standards into reliable runtime skills and Tool SOPs using a repeatable standard.

This skill is optimized for agent-native artifacts, not human-facing documentation. A good agent skill is a runtime package that helps Hermes route, load, act, stop, verify, and improve correctly. It should have:

- precise invocation metadata;
- a lean `SKILL.md`;
- progressive disclosure into `references/`, `templates/`, `scripts/`, and `assets/`;
- explicit tool/action permissions;
- side-effect and risk boundaries;
- stop/ask/escalate rules;
- deterministic scripts where useful;
- eval cases and observed-use feedback loops.

For ordinary human-facing playbooks and SOPs, use `helpful-hermes-human-playbook-sop-creator` instead.

## When to Use

Use this skill when:

- The user asks to create, fork, rewrite, or review a Hermes skill.
- The artifact should teach Hermes reusable behavior rather than only produce a human document.
- The artifact is a Tool SOP: instructions for safely using a CLI, API, repo, browser workflow, MCP server, platform, or Hermes tool.
- A workflow depends on tool permissions, side effects, scripts, validations, structured outputs, or stop/ask/escalate rules.
- A draft skill needs to be scored for invocation quality, progressive disclosure, safety, eval coverage, and runtime usefulness.
- A human playbook/SOP is becoming agent-executable and needs to graduate into skill form.

Do not use this for:

- Purely human-facing playbooks/SOPs that do not need agent runtime behavior; use `helpful-hermes-human-playbook-sop-creator`.
- General Hermes skill file syntax/frontmatter questions alone; load `hermes-agent-skill-authoring` for validator and repo conventions.
- Public publishing checks by themselves; load `thorough-hermes-skill-publishing` for private-to-public release safety.
- File routing or workspace cleanup by itself; load `tidy-hermes-workspace-hygiene`.
- One-off answers that do not create durable agent behavior.

## Runtime Contract

### Invocation Contract

Hermes should load this skill when the task is about **building or reviewing agent-runtime skill artifacts**. It may be invoked by the model when the user asks for skill creation/review, Tool SOPs, reusable agent procedures, or agent-skill standards.

Hermes should not load this skill for ordinary human-facing Playbooks/SOPs, pure file cleanup, public publishing checks, or generic planning unless the plan is specifically for a skill/tool-SOP artifact.

Neighboring-skill routing:

- `hermes-agent-skill-authoring` — validator, frontmatter, directory conventions, in-repo/user-local mechanics.
- `helpful-hermes-human-playbook-sop-creator` — human-facing Playbooks/SOPs.
- `tidy-hermes-workspace-hygiene` — git, file routing, runtime/source sync, destructive-operation guardrails.
- `thorough-hermes-skill-publishing` — public/shared release safety.

### Runtime Action Model

After loading this skill, Hermes may autonomously:

- classify whether an artifact should be an Agent Skill, Tool SOP Skill, Review Protocol, Lightweight Skill Draft, or human-facing artifact;
- review and score a pasted/path-accessible draft;
- propose skill structure, runtime contract, eval cases, support-file map, and score sheet;
- draft content in chat;
- read relevant source files and neighboring skill metadata when within scope.

Hermes may edit files only when the user has authorized creation/modification of the relevant skill/workspace and the agent has followed `tidy-hermes-workspace-hygiene` git/path checks.

Hermes must ask before:

- deleting, moving, or replacing existing skill directories/files;
- syncing installed runtime copies if the operation overwrites or removes files;
- changing public/shared repos or publishing;
- touching protected private knowledge-base wiki paths;
- making high-impact/destructive changes outside the explicitly approved scope.

### Expected Tools

Common tools:

- `skill_view` / `skills_list` — load related skills and support files.
- `read_file` / `search_files` — inspect source docs and private repo copies.
- `write_file` / `patch` — edit private source skills after authorization.
- `terminal` — git status/diff/commit, validation commands, controlled syncs.
- `delegate_task` — isolated adversarial review.
- `todo` — track multi-step skill work.

### Risk Class

Review-only use is read-only and usually autonomous.

Drafting in chat is low risk.

Private source skill edits are write-capable and require scope clarity + git safety.

Runtime installed-skill sync is write-capable and can affect future Hermes behavior; verify source/runtime match after sync.

Deletion, public publishing, protected wiki edits, credential-bearing tool instructions, and irreversible changes require explicit approval and the relevant guardrail skill.

### Stop / Ask / Escalate Rules

Continue autonomously when:

- reviewing an artifact already provided or discoverable in the approved workspace;
- drafting proposed content in chat;
- reading related skills/source docs;
- validating frontmatter or score categories.

Ask the user when:

- the intended artifact type is ambiguous and the choice changes the tool/file actions;
- file edits are needed but scope/path is not approved;
- destructive or cleanup actions are needed;
- a public/shared release is implied;
- a governance decision is needed, such as whether the owner/private policy should remain in a portable skill.

Stop immediately when:

- a path is protected private knowledge-base wiki and write scope was not explicitly approved;
- a destructive operation is denied or blocked;
- the task would publish private/local material publicly without review;
- available context is insufficient to safely edit a source-of-truth skill.

### Expected Outputs and Verification

For review tasks, output a score sheet with:

- artifact pinned: name, version, path/source, and whether runtime/private/public copy;
- standard used;
- category-by-category 0-2 scores;
- total and interpretation band;
- exact quoted gaps;
- required fixes;
- optional improvements;
- final verdict.

For creation/edit tasks, output:

- files changed;
- source/runtime relationship;
- validation evidence;
- git status/commit when applicable;
- any deferred evals, support files, or governance decisions.

## North Star Principles

1. **Skills Are Runtime Assets.** A skill is loaded because metadata matched a task, then it changes what the agent does.
2. **Progressive Disclosure Wins.** Metadata routes. `SKILL.md` guides. Support files carry detail. Scripts make repeatable operations deterministic.
3. **Trigger Precision Is Safety.** Bad names/descriptions cause over-triggering, under-triggering, collision, or dangerous automation.
4. **Actions Need Boundaries.** Every tool-capable skill should say what the agent may do, what requires approval, and when to stop.
5. **Eval Before Trust.** A polished skill is not proven until representative cases show it triggers, acts, refuses/asks, and verifies correctly.
6. **Observe Real Trajectories.** If the skill loads at the wrong time or causes bad behavior, patch the skill instead of blaming the session.
7. **Build Clean, Not Bulky.** Keep the runtime path tidy and the `SKILL.md` focused; move optional detail to support files.

## Operating Procedure

Use this sequence for skill/tool-SOP creation or review.

### Mode 1 — Review-only

1. Pin the artifact version and source: user-pasted, private repo, runtime copy, public repo, or historical version.
   - If the user refers to “first,” “original,” “yesterday,” “before the rewrite,” or “what Grok made,” do not silently score the current installed copy. Resolve the likely historical source from git/session context when available and state the commit/path scored.
   - If multiple plausible artifacts match, choose the best-supported interpretation, label it, and offer to re-score exact paths if the user meant different ones.
   - If the user asks about a skill-dev folder regression, source-library regression, duplicated skill, wrong repo placement, or redundant source-layout wrappers, inspect sibling source repos and corpus layout for duplicate copies, wrong artifact-class placement, and unnecessary `skills/` or category nesting before focusing on source/runtime drift or content scoring.
2. Choose the standard: Agent Skill, Tool SOP Skill, Review Protocol, or human-facing Playbook/SOP redirect.
3. Load related skills and support files needed for the review.
4. Run adversarial review, preferably isolated via subagent for important artifacts.
5. Score using the 0-2 rubric.
6. Quote exact gaps.
7. Recommend required fixes and optional improvements.
8. Do not edit files unless the user asked for edits and scope is safe.
9. When using a subagent reviewer, treat the subagent’s result as advisory: reconcile it against the artifact yourself before finalizing scores.

### Mode 2 — Create/draft

1. Identify the repeated agent behavior, tool capability, or failure pattern.
2. Collect representative cases before polishing: should-trigger, should-not-trigger, success, missing-context, dangerous-action, tool-unavailable, neighboring-skill collision.
3. Survey neighboring skill names/descriptions to avoid duplication and routing collision.
4. Draft metadata first: name and description are the first-level routing surface.
5. Choose runtime/source category placement deliberately before writing files. Category names should be tied to the user's domains of operation, not vague artifact-class buckets, unless the user explicitly accepts a temporary bucket. For the owner's private runtime library, `hermes-proficiencies/` is an accepted temporary replacement for the old `software-development/` catch-all for broad Hermes behavior/proficiency skills; broader OpenClaw-import taxonomy remains a high-priority governance decision to refine as skills/SOPs are imported. Do not encode a proposed taxonomy into skills if the owner rejects it; revert rejected support files/edits and keep only the accepted narrow change.
6. Draft a lean `SKILL.md` with runtime contract, procedure, support-file map, evals, pitfalls, verification, and changelog.
7. Split support files when detail is bulky, rare, historical, or mutually exclusive.
8. Add deterministic scripts when repeated operations should not depend on prose.
9. Review, fix, and re-score before trusting. If you upgraded a skill to close a scored gap, do not claim a new numeric score, readiness band, or “hardened” status unless you performed a post-patch re-score against the same pinned standard; otherwise label the result as an estimate and name the deferred verification.

### Mode 3 — Patch/edit existing skill

1. Check git status and source-of-truth path.
2. Before editing, classify the write surface:
   - **private runtime library edit** — for the owner's active private/local skills, `~/.hermes/skills/` is the canonical git-controlled working tree; edit the installed runtime skill, then review and commit the runtime-library git diff;
   - **public-bound skill-dev edit** — use `~/.hermes/skill-dev/` only for skills intended for public/shared release or publish-clean export;
   - **hub/bundled/archived/stale skill** — do not track or edit unless the user explicitly authorizes the allowed mechanism.
3. `skill_view`/`skill_manage` normally load and patch installed runtime skills. That is acceptable for the owner's tracked private runtime library because the installed skill tree is now git-controlled. It is not acceptable for public publishing without a separate clean export/review pass.
4. Prefer targeted `patch` for small edits; use full `write_file` only for intentional rewrites.
5. Preserve user-authored wording unless the edit specifically improves runtime behavior or clarity.
6. Validate frontmatter, size, support-file links, and runtime contract coverage.
7. If a skill is public-bound, export/review it from runtime into `skill-dev` or the public repo only after it works locally.
8. Verify `git diff` in `~/.hermes/skills/` and commit durable private skill-library changes.
9. Do not claim public readiness until the publishing safety workflow has checked the exported copy.

### Mode 4 — Runtime library / cleanup

1. Treat `~/.hermes/skills/` as the owner's canonical private runtime skill library when the skill is actively worked on or agent-created and tracked by git.
2. Use `~/.hermes/skill-dev/` only for skills intended for public/shared release, publish-clean export, or other non-runtime packaging work.
3. Track only active worked-on skills and generated/agent-created skills in the runtime git repo. Keep hub-installed skills, archived/stale skills, curator metadata, lockfiles, and similar runtime noise untracked.
4. Use tarball backups only for tiny one-off emergency edits; for normal private skill evolution, rely on runtime-library git status/diff/commit.
5. If replacing/deleting runtime files is needed, explain the operational reason and exact scope in the approval request.
6. Verify the tracked runtime-library git diff after edits and commit durable changes.
7. Report touched paths, whether the skill is tracked/ignored, and git status.

### Mode 5 — Public/shared publishing

Stop and load `thorough-hermes-skill-publishing`. This skill can prepare the artifact, but publishing requires the publishing safety workflow.

### Mode 6 — Post-session skill library update pass

When the user asks to review a session and update the skill library, be active by default. Treat corrections, workflow preferences, repeated tool patterns, review techniques, wrong-source recoveries, and missing skill guidance as durable skill signals unless they are clearly one-off or environment-transient.

Procedure:

1. Prefer patching a skill that was loaded or directly used in the session.
2. If no loaded skill fits, patch an existing class-level umbrella skill before creating anything new.
3. Keep the library shaped as broad class-level skills with rich `SKILL.md` files and support files for detail; this shapes how to update, not whether to update.
4. Do not create narrow one-session-one-skill artifacts, PR/error-specific skills, or session narrative skills.
5. Put user workflow/style corrections into the governing skill body, not only memory, so the future runtime behavior changes.
6. Capture the reusable fix/pattern, not transient setup failures or stale negative claims about tools.
7. Choose support-file type deliberately when detail does not belong inline:
   - `references/<topic>.md` for session-specific detail, condensed research/API notes, provider quirks, error transcripts, reproduction recipes, or source-lineage context;
   - `templates/<name>.<ext>` for copy-and-modify starters, output shapes, configs, prompts, or known-good examples;
   - `scripts/<name>.<ext>` for deterministic probes, validators, generators, packaging steps, or other statically re-runnable actions.
   Add a one-line pointer in `SKILL.md` whenever a support file is created so future agents know when to load it.
8. If the user says the session was poisoned, the wrong source/tweet/artifact was used, or says “stop” to redirect the work, do not preserve the mistaken trajectory as if it were validated learning. Capture the recovery pattern: acknowledge the reset, pin the corrected source, distinguish prior mistaken analysis from reusable process, and update the governing skill to prevent that failure class.
9. Use session history/search when the reusable learning depends on earlier context that may have been compacted, but store only the durable procedure or pitfall, not the one-off narrative.
10. If adding a support file, add a one-line pointer in `SKILL.md` explaining when to load it.
11. If the user constrains available tools for the curation pass, obey that boundary literally. Use visible conversation context and `skill_view`/`skill_manage` only when that is the allowed surface; do not attempt denied filesystem, git, session-search, terminal, or validation tools. Do not claim fresh git status, source/runtime equality, commits, file diffs, or validation evidence unless that evidence is already present in the visible conversation or was produced by an allowed tool. State which verification steps were skipped/deferred because of the declared tool boundary.
12. If a useful patch is possible under the constrained tool surface, make the skill-library update anyway rather than stalling on unavailable verification. Keep the patch narrow, append a changelog entry, and report the verification limitation explicitly.
13. If nothing genuinely reusable emerged, say `Nothing to save.` — but do not use that as the default when the user explicitly requests an active library update.

## Artifact Type Decision

Pick the artifact type before writing.

```text
If the artifact installs reusable agent behavior across a domain:
  Build an Agent Skill.

If the artifact teaches a tool, API, CLI, repo, browser flow, MCP server, or platform:
  Build a Tool SOP Skill.

If the artifact defines review/scoring of skills, tools, or agent procedures:
  Build a Review Protocol inside the relevant skill or as a dedicated skill.

If the artifact is a human-facing Playbook or SOP with no runtime/tool behavior:
  Use helpful-hermes-human-playbook-sop-creator.

If the workflow is experimental, low-risk, and not ready for durable behavior:
  Build a Lightweight Skill Draft and mark deferred eval/guardrail work explicitly.
```

### Skill Taxonomy

Use natural language first; thematic labels should clarify, not obscure.

```text
tool skills
  Plain-language default for skills that teach Hermes a tool, CLI, API,
  platform, vault, account, or local workflow.

soulbound skills
  Thematic/private subtype of tool skills: local/private skills bound to
  the owner/the local user's vaults, accounts, machines, paths, and workflows. These belong
  in the soulbound source repo and are private/local by default.

Hermes proficiencies
  Public/shareable behavior or attribute skills: tidy, thorough, methodical,
  careful, etc. These belong in the proficiencies source/library, even while
  still private.

runtime skills
  Implementation detail: any installed skill under `~/.hermes/skills/`.
  Avoid using this as a class name because all installed skills are runtime-loaded.
```

Classification pitfall: do not place a Hermes proficiency in the soulbound/tool-skill source repo merely because it needs private git history. Repo/source placement should follow artifact type, not just privacy level.

## Progressive Disclosure

This skill keeps the core runtime standard in `SKILL.md` because it is usually needed when building or reviewing agent skills. Support files carry background or reusable templates.

Support files:

- `references/agent-skill-native-guidance.md` — distilled Anthropic Agent Skills / Claude Code Skills and OpenAI GPT-5 / Agents guidance that motivated this standard.
- `references/credential-tool-sop-porting-notes.md` — rules for converting password-manager, secret-vault, sudo-access, API-key, and credential SOPs into Hermes Tool SOP skills without leaking private identifiers or losing anti-secret-exposure guardrails.

### Support File Format Selection

Choose support-file formats by operational purpose, not convenience:

- **Markdown (`.md`)** — narrative procedures, human/agent context, source-lineage notes, examples, and mode references. Use when prose and judgment are the value.
- **YAML (`.yaml`/`.yml`)** — structured configuration, mode maps, checklists, option sets, and values that humans should edit safely. Use when comments and readability matter.
- **JSONL (`.jsonl`)** — append-only ledgers for decisions, eval runs, review results, failure observations, and historical events. Use when preserving chronology matters and agents should add records without rewriting history.
- **Scripts (`scripts/`)** — deterministic validation, API calls, transforms, packaging, scoring helpers, and repeatable checks. Use when prose would create brittle manual execution.
- **Templates (`templates/`)** — copyable output shapes, score sheets, prompts, config starters, or request bodies. Use when the artifact should be reused but not treated as factual history.
- **Assets (`assets/`)** — images, diagrams, fixtures, screenshots, or binary examples that are required only in specific modes.

If a support file records skill evolution or review outcomes, prefer JSONL over repeatedly rewriting Markdown. If a process is executed more than twice or must be exact, promote it from prose to a script.

### Mode Router Pattern

When a skill has multiple modes, frameworks, tools, audiences, risk classes, or sub-procedures, make `SKILL.md` a compact router plus common workflow. Put mode-specific details in support files and instruct Hermes to load only the selected file.

Recommended router shape:

```text
Task signal / problem signal / user intent → Mode → Support file → Escalation or fallback
```

Mode support files should be self-contained enough to execute the mode without loading every other mode. Each mode file should include:

- when this mode applies;
- exact procedure;
- allowed tools/actions;
- stop/ask/escalate rules;
- verification evidence;
- common failure modes or limitations;
- when to escalate to another mode.

Design test: from `SKILL.md` alone, Hermes should be able to choose the correct mode/reference file. It should not need to read every support file just to decide what to do.

Use a router especially when `SKILL.md` is trending toward a long bundle of independent procedures. This is the agent-skill version of progressive disclosure: route first, reveal details on demand.

### Gradient Design Pattern

For broad proficiency skills, progressive disclosure should behave like a **gradient** rather than a binary split between “main file” and “references.” Keep the always-needed operating layer in `SKILL.md`, then reveal deeper support files as task risk, specificity, or complexity increases.

Recommended gradient shape:

```text
Base layer: SKILL.md
  Metadata, trigger/counter-trigger, runtime contract, expected tools, risk classes,
  mode router, core workflow, short evals, key failure modes.

Layer 1: Common mode support
  Normal/common execution paths that are too detailed for every invocation.

Layer 2: Risk or domain mode support
  Protected paths, destructive operations, publishing, credentials, source/runtime sync,
  browser automation, external side effects, or other high-consequence branches.

Layer 3: Shared templates/scripts
  Verification checklists, score sheets, deterministic validators, copyable configs,
  or scripts that make repeated exact work safer.

Layer 4: Historical/source-lineage references
  Incident notes, original source excerpts, transcripts, upstream docs, or rationale that
  should not be loaded unless auditing or evolving the skill.
```

Use gradient design when the user wants to “step on the gas” without making a mess: the base skill should be small enough to steer fast routine work, while high-risk modes have enough detail to prevent regressions. The refactor target is not merely a shorter `SKILL.md`; it is correct **activation depth**. Future agents should load no more than the task needs and no less than safety requires.

Recommended future support files when this skill grows:

- `templates/score-sheet.md` — copyable review output template.
- `templates/eval-cases.md` — copyable eval-case skeleton.
- `templates/tool-sop.md` — Tool SOP starter.
- `templates/agent-skill.md` — Agent Skill starter.
- `scripts/validate_skill.py` — deterministic frontmatter/link/size validation if repeated manual validation becomes brittle.

Rules:

- If `SKILL.md` grows with long examples, source excerpts, historical rationale, detailed templates, or mutually exclusive modes, move that material to support files and link it here by purpose.
- Do not load every support file by default. Load only the file(s) selected by the router plus any shared reference needed for the task.
- If a skill contains 3+ distinct modes or frameworks, require a router table/list unless there is a documented reason not to split.

## Agent Skill Standard

Use this for general Hermes skills that install reusable agent behavior.

### Required Shape

```markdown
---
name: <skill-name>
description: Use when <specific trigger>. <runtime behavior/capability this installs>.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [<tags>]
    related_skills: [<related-skills>]
---

# <Skill Title>

## Overview

What behavior this skill installs and why it exists.

## When to Use

- Trigger conditions
- Counter-triggers / when not to use
- Related skills to use first/instead

## Runtime Contract

Invocation, action model, risk class, stop/ask/escalate rules, outputs, verification.

## Operating Procedure

Concrete steps Hermes should take when the skill is loaded.

## Progressive Disclosure

- `references/...` — when to load and why
- `templates/...` — when to use and expected output
- `scripts/...` — when to run and what it does
- `assets/...` — when needed

## Eval Cases

Minimal should-trigger / should-not-trigger / success / missing-context / dangerous-action cases.

## Common Pitfalls

- **Pitfall:** What goes wrong
  **Fix:** What to do instead

## Verification Checklist

- [ ] Checklist proving the skill is ready

## Changelog

- 1.1.10 — 2026-05-27 — Strengthened tool-bound post-session curation behavior: when the user limits the pass to memory and skill-management tools, update the skill library through allowed tools only, avoid denied git/filesystem/session-search validation, and explicitly disclose deferred verification instead of overclaiming evidence. Why: the owner’s curation prompt intentionally constrained the tool surface while still requiring active skill updates.
- 1.1.9 — 2026-05-27 — Added explicit create/draft category-placement step and tool-boundary rule for post-session curation passes. Why: the owner asked for active skill-library updates while restricting the tool surface to memory/skill tools, and earlier work showed runtime/source category placement must be a deliberate artifact-class decision rather than a default to `software-development`.
- 1.1.8 — 2026-05-27 — Added category/source placement as an explicit skill-creation decision and failure mode. Why: the owner identified that broad Hermes proficiencies had been placed under the runtime `software-development` category even though they are not limited to software development; future skill creation should use a Playbook/SOP-style taxonomy decision before choosing runtime/source folders.
- 1.1.7 — 2026-05-27 — Added redundant-wrapper source-layout regression guidance. Why: the owner identified that `hermes-proficiencies/skills/software-development/` copied runtime/category layout into the private source repo; future skill-dev audits should classify repo purpose and detect unnecessary wrapper folders before scoring prose quality.
- 1.0 — YYYY-MM-DD — What changed. Why: <context/trigger>. Reference: <URL/path/session note>.
```

### Agent Skill Quality Bar

An Agent Skill is not done until:

- [ ] Name and description are specific, routing-useful, and not collision-prone.
- [ ] Counter-triggers say when not to use it.
- [ ] Runtime Contract is explicit.
- [ ] Tool/action permissions and side-effect boundaries are clear.
- [ ] `SKILL.md` is lean; support files carry bulky detail.
- [ ] Support-file formats match purpose: Markdown for narrative/context, YAML for human-editable structure, JSONL for append-only ledgers, scripts for deterministic checks, templates for reusable shapes, and assets for fixtures/media.
- [ ] If the skill has 3+ modes/frameworks/sub-procedures, `SKILL.md` includes a router table/list and mode-specific support files.
- [ ] Any deterministic repeated operation is a script or has a reason not to be.
- [ ] Expected outputs and verification evidence are explicit.
- [ ] Minimal eval cases exist or are explicitly deferred under lightweight rules.
- [ ] Common pitfalls come from real or plausible agent failures.
- [ ] Related skills are listed and do not create ambiguous routing.

## Tool SOP Skill Standard

Use this for tools, APIs, CLIs, repos, platforms, browsers, MCP servers, Hermes tools, and other agent capabilities.

Tool SOPs optimize for fast correct execution under context pressure. They should emphasize when to use the tool, what it gives you, exact patterns, safe defaults, and gotchas from real failures.

### Required Shape

```markdown
---
name: <tool-or-capability-name>
description: Use when <trigger involving this tool/capability>. <what capability this unlocks and when it beats alternatives>.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [tool-sop, <tool-name>]
    related_skills: [<related-skills>]
---

# <Tool Name> Tool SOP

## Quick Ref

- Commands, endpoints, paths, env vars, tool calls, or API shapes
- Keep this usable in 10 seconds

## When to Use This

If/then decision tree covering:

- What this tool gives Hermes
- When it beats alternatives
- When not to use it
- Expected outputs and failure signals

## Runtime Contract

Allowed actions, forbidden actions, risk class, approval thresholds, stop/ask/escalate rules.

## Usage Patterns

### Pattern name

Exact steps, commands, tool calls, or request examples.

## Verification / Health Checks

How to confirm the tool call, command, or workflow worked.

## Gotchas & Lessons

- **What went wrong:** What to do instead.
- Reference real incidents or failure modes when possible.

## Support Files

- `references/...` for detailed docs or API notes
- `templates/...` for request/response bodies or config starters
- `scripts/...` for deterministic workflows

## Changelog

- 1.0 — YYYY-MM-DD — What changed. Why: <context/trigger>. Reference: <URL/path/session note>.
```

### Tool SOP Quality Bar

- [ ] Quick Ref is usable in 10 seconds.
- [ ] When-to-use decision tree says what the tool gives Hermes, not just what it does.
- [ ] Usage patterns are executable, not conceptual.
- [ ] Tool/action permissions are clear enough for autonomous vs approval-required behavior.
- [ ] Side effects, credentials, privacy, public posting, destructive writes, and cost risks are guarded.
- [ ] Stop/ask/escalate rules cover missing access, ambiguous target, dangerous action, and tool failure.
- [ ] Verification commands or checks prove success.
- [ ] Deterministic scripts are included under `scripts/` when they would make repeated execution safer or less ambiguous.
- [ ] Code blocks are labeled as executable commands/scripts or illustrative references.
- [ ] Gotchas are practical and specific.

## Skill Creation Procedure

1. **Identify the repeated agent behavior.** What task, failure, tool use, or decision pattern should survive this session?
2. **Collect representative cases.** Include at least one should-trigger, should-not-trigger, success, missing-context, tool-unavailable, neighboring-skill collision, and dangerous-action scenario.
3. **Survey neighboring skills.** Check names/descriptions to avoid duplicate or collision-prone triggers.
4. **Draft metadata first.** Name and description are the first-level routing surface. Make them specific.
5. **Draft the lean `SKILL.md`.** Include only instructions needed on most invocations.
6. **Split support files.** Move large references, templates, scripts, examples, and source-lineage notes out of `SKILL.md`.
7. **Add Runtime Contract.** Define actions, tools, risk class, approval thresholds, stop rules, outputs, and verification.
8. **Add eval cases.** Write minimal cases even if they are manual checks at first.
9. **Review adversarially.** Score against the Review Protocol below.
10. **Sync source and runtime.** Keep private source repo and installed `~/.hermes/skills/` copies reconciled when this is a shareable/important skill.
11. **Observe and patch.** After real use, update the skill if invocation or trajectory was wrong.

## Lightweight Skill Drafts

Use only when the process is low-risk, early-discovery, and not trusted for high-stakes behavior.

Required rules:

- Mark it clearly as `Provisional / Eval Needed`.
- Include at minimum: Overview, When to Use, Operating Procedure, Stop/Ask rules, Changelog.
- Explicitly list deferred work: support files, eval cases, scripts, safety review.
- Do not use for critical, external-facing, financial, legal, safety, credential, destructive, public publishing, or irreversible workflows.

## Eval Cases

Use these to test this skill and as a minimum model for new agent skills.

### Should trigger

User asks: “Create a Tool SOP skill for using xurl safely.”

Expected behavior: load this skill, classify as Tool SOP Skill, survey related skills/tool docs, draft runtime contract, usage patterns, eval cases, guardrails, and verification.

### Should not trigger

User asks: “Write a human SOP for our weekly family planning meeting.”

Expected behavior: route to `helpful-hermes-human-playbook-sop-creator`, not this skill.

### Successful completion

User provides a draft agent skill and asks for review.

Expected behavior: pin artifact version, choose Agent Skill standard, score every category 0-2, quote exact gaps, total the score, and recommend fixes.

### Upgrade and re-score

User asks to bring an existing skill up to spec after an initial score.

Expected behavior: pin the pre-change score and standard, patch the gaps, then run or explicitly defer a post-patch re-score. Do not present a fresh numeric score or “fully hardened” verdict as fact unless the re-score actually happened; if tool or time limits block re-scoring, say which verification is deferred.

### Gradient refactor

User asks whether a skill follows progressive disclosure or says a refactor would make it more “gradient design.”

Expected behavior: treat this as a methodical skill-design task. Preserve the base runtime contract and mode router in `SKILL.md`; move mode-specific detail to `references/modes/`; move reusable output shapes to `templates/`; move deterministic repeated checks to `scripts/`; add a support-file map; then verify the main skill can select the right depth without loading every support file.

### Historical artifact review

User asks: “Score the first two skills Grok made yesterday against the new skill.”

Expected behavior: infer that the user likely means the original historical skill versions, inspect git/session context when available, pin the exact commit and paths scored, state the assumption, and offer to re-score different exact artifacts if needed. Do not score the already-improved current runtime copies without saying so.

### Skill-library regression / duplicate placement

User asks: “Look at the regression of the skill-dev folder,” corrects that “the main problem is the skill is in both folders,” or says an extra `skills/software-development/` wrapper is redundant.

Expected behavior: audit the skill-library structure before scoring prose quality. Check whether the same skill exists in multiple source repos, whether its artifact class matches its repo (`Hermes proficiencies` vs `soulbound/tool skills`), whether both copies are tracked, whether redundant source-layout wrappers exist, and whether runtime/source drift is secondary to wrong canonical placement. Report exact duplicate/redundant paths and clean only after explicit deletion/move scope approval.

### Wrong-source / poisoned-context recovery

User says: “stop, I gave you the wrong tweet/source” or “the session was poisoned; do you recall the earlier context?”

Expected behavior: immediately stop extending the mistaken analysis, acknowledge the corrected source/context boundary, pin the new source before reviewing it, and separate the prior wrong-source work from reusable process learning. If earlier context matters and may have been compacted, use session history/search to recover only the relevant durable context before answering or patching skills.

### Tool-bound curation pass

User says: “Review the conversation above and update the skill library. You can only call memory and skill management tools.”

Expected behavior: load the governing skill with `skill_view`, patch the most relevant loaded/class-level skill via `skill_manage` if a reusable learning exists, and do not call terminal, filesystem, git, session-search, todo, or validation tools. Report that source/runtime equality, git status, commits, and external validation were not freshly checked due to the declared tool boundary unless visible context already contains that evidence.

### Missing context

User says: “Fix that skill from yesterday” with no name/path and no retrievable context.

Expected behavior: use session search or ask for the exact skill/path before editing. Do not guess or edit unrelated skills.

### Dangerous action / approval required

User asks to “replace the installed runtime skill with the new one.”

Expected behavior: check private source and runtime paths, explain reason/scope before any delete/overwrite, request approval if deletion/overwrite is required, then verify private/runtime match.

### Tool unavailable / dependency missing

A skill references a CLI or script but the command is not installed.

Expected behavior: mark setup gap, include installation/setup requirement or fallback, and do not claim the Tool SOP is ready.

### Neighboring-skill collision

A draft skill description says “Use when creating SOPs.”

Expected behavior: flag collision with `helpful-hermes-human-playbook-sop-creator`; narrow to agent-runtime skills or human-facing SOPs.

## Review Protocol

Run this before trusting an Agent Skill, Tool SOP, or skill-quality rubric.

### 0. Pin the Artifact Version

Before scoring, identify exactly which artifact is under review:

- Current installed/runtime version
- Private source-repo version
- Public repo version
- Original historical version from session history/git
- User-pasted draft

If the user refers to a historical artifact but the installed copy has since been patched, state which version you are scoring and offer to score the historical original separately.

### 1. Choose the Scoring Standard

```text
What was built: Agent Skill
Score against: Agent Skill Standard + Hermes skill frontmatter rules

What was built: Tool SOP Skill
Score against: Tool SOP Skill Standard + tool-specific docs/constraints

What was built: Review Protocol
Score against: this Review Protocol + intended artifact type

What was built: Human-facing Playbook/SOP
Stop and switch to helpful-hermes-human-playbook-sop-creator

What was built: Publishing-ready public skill
Score against: this standard + thorough-hermes-skill-publishing
```

### 2. Run Adversarial Review

For agents, spawn a subagent or run an isolated review pass with only:

- the draft artifact;
- the relevant standard;
- neighboring skill names/descriptions when possible;
- exact scoring instructions.

Reviewer instruction:

```text
Score every section strictly. Flag exact violations with quotes. Do not be nice. Identify over-triggering, under-triggering, neighboring-skill collisions, missing runtime boundaries, unclear tool permissions, unsafe side effects, missing stop rules, weak evals, poor progressive disclosure, non-portable assumptions, and places where Hermes would get stuck or over-act.
```

### 3. Score the Artifact

Use a 0-2 scale per category:

```text
0 = Missing or unsafe
1 = Present but vague, incomplete, fragile, or untested
2 = Complete, clear, executable, safe, and maintainable
```

Core categories:

- Trigger clarity: When to use / not use is obvious.
- Frontmatter routing quality: Name and description are specific, non-colliding, and not over/under-triggering.
- Objective clarity: Runtime behavior and success can be judged.
- Structure compliance: Uses Agent Skill or Tool SOP shape correctly.
- Runtime contract: Invocation boundaries, allowed actions/tools, stop/ask/escalate rules, expected outputs, and verification are explicit.
- Progressive disclosure: `SKILL.md` is lean and support files hold detailed references, templates, scripts, examples, or source lineage. Multi-mode skills include a compact router and load only the selected reference file(s). Support-file formats are chosen by purpose rather than convenience.
- Executability: Hermes can run the procedure under realistic context pressure.
- Tool/action safety: Side effects, credentials, privacy, destructive steps, public posting, cost, and approval thresholds are guarded.
- Eval coverage: Should-trigger, should-not-trigger, missing-context, dangerous-action, tool-unavailable, and successful-completion cases exist or are explicitly deferred for a lightweight draft.
- Verification: Quality checks prove real outcomes.
- Portability: No accidental private paths, IDs, user-specific assumptions, or local-only references unless explicitly marked private.
- Maintainability: Changelog entries explain what changed, why it changed, and cite reference links/paths/session context when available; related skills, support files, failure modes, and post-use audit support updates.
- Parent feedback: New learnings are fed back to parent playbooks, related skills, or tool SOPs.

Interpretation:

```text
22-26 = Excellent. Ready after final owner review.
17-21 = Usable draft. Fix flagged issues before relying on it.
11-16 = Weak. Needs structural rewrite.
0-10  = Not acceptable. Rebuild from source.
```

### 4. Score Sheet Template

```markdown
## Score Sheet: <artifact>

Artifact pinned:
- Name:
- Version/source:
- Path or pasted draft:
- Standard used:

Scores:
- Trigger clarity: <0-2> — <reason>
- Frontmatter routing quality: <0-2> — <reason>
- Objective clarity: <0-2> — <reason>
- Structure compliance: <0-2> — <reason>
- Runtime contract: <0-2> — <reason>
- Progressive disclosure: <0-2> — <reason>
- Executability: <0-2> — <reason>
- Tool/action safety: <0-2> — <reason>
- Eval coverage: <0-2> — <reason>
- Verification: <0-2> — <reason>
- Portability: <0-2> — <reason>
- Maintainability: <0-2> — <reason>
- Parent feedback: <0-2> — <reason>

Total: <N>/26 — <band>

Exact quoted gaps:
1. “...” — why it matters

Required fixes:
1. ...

Optional improvements:
1. ...

Final verdict:
...
```

### 5. Short Score Output Mode

When the user asks for a short result, quick score, compact verdict, or “just the answer,” do not emit the full score sheet. Still perform the review discipline internally, but deliver only:

- total score and interpretation band;
- 1-3 point deductions or top gaps;
- final verdict / approval caveat.

Use the full score sheet only when the user asks for detail, the artifact is high-risk, the result is disputed, or exact quoted gaps are needed to drive edits.

### 6. Fix and Re-score

- Fix every gap flagged by the review.
- Re-score after fixes; fixing one issue can break another.
- Save or summarize the score sheet when the artifact is important.
- If updating a tool SOP exposes a parent skill gap, update and re-score the parent.

### 7. Reviewer Loop

1. Owner/agent produces draft.
2. Adversarial review flags issues.
3. Owner/agent fixes issues.
4. Reviewer inspects final version.
5. Repeat until approved or explicitly accepted as a lightweight draft.

Root-standard exception: this standard itself should receive direct owner review before being treated as fully authoritative, because it governs the review loop and can otherwise grade its own logic. In the owner’s private skill library, the owner is the root-standard reviewer.

### 8. Locked Evaluator / Anti-Gaming Rule

Do not let the same edit both weaken the scoring standard and pass because of the weakened standard. When a change modifies a rubric, score band, evaluator instruction, required eval case, or approval threshold:

1. Pin the pre-change evaluator text before editing.
2. State whether the change strengthens, clarifies, narrows, or weakens the standard.
3. Review the artifact against the pre-change standard first unless the owner explicitly approves changing the standard before scoring.
4. If the standard must change, run a second review against the new standard and disclose both results or the reason the old score is obsolete.
5. Do not remove hard cases, dangerous-action evals, counter-triggers, or verification requirements merely to make a skill pass.
6. For root standards, request the owner's review for material rubric changes before treating the updated standard as authoritative.

Evaluator changes are allowed when they improve truth and safety. They are not allowed as a way to launder a weak artifact into a passing score.

## Parent Feedback Procedure

When review or use exposes a gap:

1. Identify the affected parent or neighboring skill.
2. Classify the gap: trigger collision, missing runtime boundary, missing eval, tool gotcha, publishing/privacy risk, workspace hygiene issue, or human/agent artifact confusion.
3. Patch the governing skill only when edit scope is authorized.
4. If not authorized, report the gap as a recommended patch with exact target skill/path.
5. Re-score the changed artifact and any parent skill whose standard changed.

Default parent/neighbor targets:

- Human-facing artifact confusion → `helpful-hermes-human-playbook-sop-creator`.
- Skill syntax/frontmatter conventions → `hermes-agent-skill-authoring`.
- Runtime/source sync and deletion guardrails → `tidy-hermes-workspace-hygiene`.
- Public release safety → `thorough-hermes-skill-publishing`.
- Agent skill/tool SOP quality standard → this skill.

## Common Failure Modes

1. **Polished document, weak runtime skill.** A skill can look good to a human while failing at routing, acting, stopping, or verifying.
2. **Frontmatter treated as decoration.** Name and description are routing surfaces. Review them adversarially.
2a. **Category treated as decoration or over-abstracted.** Runtime category folders shape browsing and agent mental routing. Review category/source placement as part of skill quality, especially when a skill is broader than a familiar bucket like `software-development`. But do not replace one bad catch-all with vague artifact-class buckets if the user wants categories tied to domains of operation. Treat rejected taxonomy proposals as non-learning: remove the rejected draft/support file and preserve only the accepted narrow rule or future governance item.
3. **Everything stuffed into `SKILL.md`.** Move large examples, detailed references, rare branches, historical context, source notes, and mutually exclusive modes into support files.
3a. **Progressive disclosure without a gradient.** A skill adds a support file but still keeps risk/domain branches tangled in the main file, so agents either under-load safety detail or over-load everything. Use a base contract + mode router + common workflow in `SKILL.md`, then route to `references/modes/`, `templates/`, and `scripts/` by activation depth.
4. **No mode router.** Multi-mode skills without a compact router force Hermes to load or reason across every procedure every time; add a signal → mode → support-file map.
5. **No counter-trigger.** The agent knows when to use the skill but not when to avoid it.
6. **Tool SOP without when-to-use.** A command list is not enough. Hermes needs to know when the tool is the right tool.
7. **Credential Tool SOP without anti-leak rules.** Password-manager and secret-vault SOPs are not ready if they only show how to retrieve secrets. Merge in secret-handling rules, mark private vault/item IDs as private or template them, forbid plaintext secret output, and add verification patterns that use counts, hashes, exit codes, or last-4 only.
8. **Tool permissions are implicit.** If autonomous vs approval-required actions are not named, the skill is unsafe.
9. **No stop conditions.** The agent continues into ambiguity or risk because the skill never says when to pause.
10. **No evals.** A review score without representative cases is aesthetic, not behavioral.
11. **Scripts are ignored.** Deterministic repeated operations stay as prose and become brittle.
12. **Code blocks are ambiguous.** The agent cannot tell whether a snippet is executable, illustrative, or historical.
13. **Neighboring-skill collision.** Similar skills with broad descriptions cause inconsistent routing.
14. **Privacy confused with artifact type.** A private proficiency is still a proficiency; a soulbound skill is a private/local tool skill bound to accounts, machines, vaults, paths, or workflows. Choose source repo and naming from artifact type first, then privacy/publishing status second.
15. **Observed failures stay local.** Bad invocation or tool behavior must patch the skill; do not treat it as a one-off.
16. **Private material leaks into shareable skills.** Load `thorough-hermes-skill-publishing` before any public repo sync.
17. **Human Playbook/SOP material pollutes runtime skill.** If the artifact is mainly for humans, route it to `helpful-hermes-human-playbook-sop-creator`.
18. **Current-copy review masquerades as historical review.** When the user asks about original/earlier/yesterday/first versions, do not score the improved installed copy by accident. Pin the historical commit/source, state the assumption, and offer to re-score exact paths.
19. **Builder edits without source/runtime discipline.** Serious skills should be developed in private source, installed to runtime for validation, and reconciled before publishing.
19a. **Native skill tools mistaken for publishing-source tools.** `skill_view` and `skill_manage` operate on installed runtime skills first. For the owner's private tracked runtime library, that is now the desired source-of-truth path; for public/shared publishing, it is not enough. Before any durable skill edit, identify whether this is a private runtime-library change, an ignored hub/bundled skill, or a public-bound export; use runtime git for private local skills and a clean `skill-dev`/publish workflow only for public-bound artifacts.
20. **Passive skill-curation pass.** When asked to update the skill library after a session, doing nothing by default loses reusable learning. First look for a loaded or governing class-level skill to patch, then add support-file detail if needed; only create a new skill when no umbrella exists.
21. **Wrong-source momentum.** If the user corrects the source, says “stop,” or calls the session poisoned, do not keep building on the mistaken artifact. Reset the task boundary, pin the corrected source/context, and capture only the recovery pattern as reusable learning.
22. **Wrong support-file format.** Agents rewrite history in Markdown logs or bury deterministic checks in prose. Choose formats by purpose: JSONL for append-only ledgers, scripts for repeatable checks, YAML for structured human-editable config, Markdown for narrative context.
23. **Evaluator gaming.** A skill weakens its own rubric, removes hard eval cases, or narrows score bands and then claims to pass. Pin the pre-change evaluator, review against it first, disclose material rubric changes, and require owner review for root-standard changes.
24. **Duplicate-source blind spot.** A review can correctly notice source/runtime drift while missing the real regression: the same skill is tracked in two source repos. When a user says folder/library regression, audit canonical placement and duplicate copies across sibling source repos before scoring content quality.
25. **Runtime-layout wrapper copied into source repo.** Source repos can drift by nesting skills under redundant category folders (`skills/software-development/<skill-name>/`) because runtime uses that shape. Classify the repo purpose first: a private skill-source repo should usually keep each skill at the repo root unless intentionally mirroring a package/runtime layout.
26. **Redundant source-layout wrappers.** A private skill source repo can drift from the intended routing model by adding unnecessary `skills/` or category folders. For `hermes-proficiencies`, check whether skills should live flat at repo root before preserving inherited runtime/upstream folder nesting.
27. **Full score sheet when user asked for short result.** Detailed review output can be correct but still fail the requested interface. If the user asks for a short score/result, keep the score sheet discipline internal and deliver only total, top deductions, and verdict.
28. **Verification overclaim under tool constraints.** In a constrained curation pass, the agent patches a skill correctly but then claims git/source/runtime validation it was not allowed to perform. Obey the declared tool surface, do the narrow allowed update, and state which verification remains deferred instead of inventing fresh evidence.
29. **Post-upgrade score laundering.** A skill receives a real pre-change score, gets patched, and the agent reports a higher score or hardened verdict without re-running the rubric. Treat post-patch readiness as unverified until a re-score is performed; if giving a rough estimate, label it as an estimate and name the missing verification.

## Verification Checklist

Before calling an Agent Skill or Tool SOP done:

- [ ] Correct artifact type selected.
- [ ] Hermes skill frontmatter is valid.
- [ ] Description is ≤1024 chars and starts with a concrete `Use when...` trigger.
- [ ] Trigger and counter-trigger conditions are clear.
- [ ] Name/description checked for over-triggering, under-triggering, and neighboring collisions.
- [ ] Runtime Contract is satisfied.
- [ ] Operating Procedure tells Hermes what to do when the skill loads.
- [ ] Progressive disclosure is used: `SKILL.md` is lean enough; detailed references, templates, scripts, and assets live in support files.
- [ ] Gradient design is appropriate for broad proficiency or high-risk skills: the base skill handles routine work quickly, mode files handle risk/domain depth, templates/scripts handle repeatable exact outputs/actions, and historical references stay out of the default path.
- [ ] Support files use the right format for their purpose: Markdown narrative, YAML structure, JSONL append-only ledgers, scripts for deterministic checks, templates for reusable output shapes, and assets for fixtures/media.
- [ ] Multi-mode skills have a router table/list that lets Hermes choose the right support file without loading all references.
- [ ] Tool/action permissions and side-effect boundaries are explicit.
- [ ] Stop/ask/escalate rules are explicit for ambiguous, risky, unavailable, or high-impact steps.
- [ ] Expected outputs and verification evidence are explicit.
- [ ] Minimal eval cases exist or are explicitly deferred under lightweight rules.
- [ ] Score Sheet Template is used for important reviews, unless the user explicitly requests a short score/result.
- [ ] Short score requests still preserve the internal review discipline but deliver only score, top gaps, and verdict.
- [ ] Failure modes/gotchas are practical and specific.
- [ ] Related parent skills or tool SOPs are updated or recommended for update.
- [ ] Changelog entries include what changed, why it changed, and reference links/paths/session context when available.
- [ ] Adversarial review was run or explicitly deferred under lightweight rules.
- [ ] If the rubric/evaluator changed, the locked-evaluator rule was followed: pre-change standard pinned, old/new scoring disclosed when relevant, and no hard cases removed to make the artifact pass.
- [ ] If the artifact was patched in response to a score, a post-patch re-score was performed or the final score/readiness claim is explicitly labeled as an estimate with deferred verification named.
- [ ] Score is acceptable for the risk level.
- [ ] Private source repo and installed runtime copy are reconciled if this skill is installed locally.
- [ ] Public publishing checks are run separately before any public repo sync.

## Changelog

- 1.1.16 — 2026-05-27 — Strengthened active post-session curation guidance: class-level/library shape affects how to update, not whether to update, and support-file creation must choose `references/`, `templates/`, or `scripts/` by operational purpose with a pointer from `SKILL.md`. Why: the owner reiterated that most sessions should produce at least one class-level skill update and that support files should preserve reusable detail without creating one-session skills.
- 1.1.15 — 2026-05-27 — Added category-taxonomy correction: the owner rejected vague artifact-class buckets as the final structure and prefers runtime categories related to domains of operation; `hermes-proficiencies/` is only the accepted narrow replacement for the `software-development/` catch-all for broad Hermes proficiency skills, while the larger OpenClaw import taxonomy remains a high-priority governance decision. Why: the initial proposal over-abstracted categories before enough OpenClaw imports were classified.
- 1.1.14 — 2026-05-27 — Switched the owner's private skill-library source-of-truth model from separate `skill-dev` private source repos to a git-controlled `~/.hermes/skills/` runtime library for active/private and generated skills, reserving `skill-dev` for public-bound export/publishing work. Why: the owner chose the simpler architecture because Hermes natively loads and patches installed runtime skills; making runtime git-controlled removes source/runtime drift while still requiring clean export before public release.
- 1.1.13 — 2026-05-27 — Added explicit warning that `skill_view`/`skill_manage` are installed-runtime-first surfaces, not canonical private-source editors; durable private-source-first skill changes must identify the source-of-truth path, edit source first with file/source-repo tools, then sync and verify runtime equality. Why: the owner identified recurring drift where runtime skill copies advanced because native Hermes skill tools made runtime patching the path of least resistance, fighting the private-source-first proficiency workflow.
- 1.1.12 — 2026-05-27 — Added explicit gradient-design guidance for progressive disclosure: base `SKILL.md` as runtime contract/mode router, mode-specific details under `references/modes/`, reusable outputs under `templates/`, deterministic checks under `scripts/`, and historical/source-lineage material as deeper references. Why: while refactoring `tidy-hermes-workspace-hygiene`, the owner identified that true progressive disclosure should let Hermes “step on the gas” with lightweight defaults while revealing deeper guardrails only as risk/complexity increases.
- 1.1.10 — 2026-05-27 — Strengthened tool-bound post-session curation behavior: when the user limits the pass to memory and skill-management tools, update the skill library through allowed tools only, avoid denied git/filesystem/session-search validation, and explicitly disclose deferred verification instead of overclaiming evidence. Why: the owner’s curation prompt intentionally constrained the tool surface while still requiring active skill updates.
- 1.1.9 — 2026-05-27 — Added explicit create/draft category-placement step and tool-boundary rule for post-session curation passes. Why: the owner asked for active skill-library updates while restricting the tool surface to memory/skill tools, and earlier work showed runtime/source category placement must be a deliberate artifact-class decision rather than a default to `software-development`.
- 1.1.8 — 2026-05-27 — Added category/source placement as an explicit skill-creation decision and failure mode. Why: the owner identified that broad Hermes proficiencies had been placed under the runtime `software-development` category even though they are not limited to software development; future skill creation should use a Playbook/SOP-style taxonomy decision before choosing runtime/source folders.
- 1.1.7 — 2026-05-27 — Added redundant source-layout wrapper regression guidance. Why: the owner clarified that `hermes-proficiencies/skills/software-development/<skill-name>/` was also wrong; private proficiencies source should be flattened to root-level skill directories while runtime keeps category folders.
- 1.1.6 — 2026-05-27 — Added skill-library regression / duplicate-placement review guidance. Why: the owner corrected a review that focused on source/runtime drift and content score while missing the real regression: `tidy-hermes-workspace-hygiene` existed in both the Hermes proficiencies source repo and the soulbound/tool-skill repo. Future reviews of skill-dev folder regressions should audit duplicate source placement and artifact-class repo fit before scoring prose quality. Reference: the originating design session on tidy skill duplicate cleanup.
- 1.1.5 — 2026-05-27 — Added short score output mode and a failure-mode/checklist reminder to preserve concise user-requested review output. Why: the owner asked to score this skill against itself and explicitly requested “Deliver me a short result”; future scoring passes should keep review rigor internally while matching the requested compact interface.
- 1.1.4 — 2026-05-27 — Added support-file format selection and locked-evaluator / anti-gaming rules, with scoring, checklist, and failure-mode coverage. Why: the owner agreed these upgrades should be added after reviewing the gradient/process discussion; future skills should use Markdown/YAML/JSONL/scripts/templates/assets intentionally and must not weaken rubrics to manufacture passing scores. Reference: the originating design session around Koylan gradient/process review.
- 1.1.3 — 2026-05-27 — Added wrong-source / poisoned-context recovery guidance to the post-session update mode, eval cases, and common failure modes. Why: the owner corrected a mistaken tweet/source and asked whether earlier Playbook/SOP context could be recovered after a poisoned session; future skill-curation passes should stop the mistaken trajectory, pin corrected sources, use session history when needed, and save only the durable recovery pattern.
- 1.1.2 — 2026-05-27 — Added the Mode Router progressive-disclosure pattern, strengthened progressive-disclosure scoring/verification, and required changelog entries to capture both what changed and why with reference links/paths/session context when available. Why: the owner reviewed Cathryn Lavery's progressive-disclosure tweet and example repo, which showed a 55-line router plus on-demand references as a practical way to cut prompt load without losing capability. References: https://x.com/cathrynlavery/status/2033960155574886509 and https://github.com/cathrynlavery/problem-solver-skill.
- 1.1.1 — 2026-05-27 — Added active post-session skill-library update mode: prefer patching loaded or class-level umbrella skills, embed user workflow corrections in skill bodies, avoid one-session skills, and reserve `Nothing to save.` for genuinely empty sessions. Why: the owner wanted skill-library curation to actively preserve reusable workflow corrections instead of letting session learnings disappear.
- 1.1.0 — 2026-05-27 — Renamed from `disciplined-hermes-skill-tool-standard` to `methodical-hermes-skill-tool-builder`; added self-specific runtime contract, operating procedure, progressive disclosure map, eval cases, score sheet template, parent feedback procedure, and local/root reviewer clarification. Why: self-review scored the prior standard 15/26 and showed it documented a rubric but did not yet operate as a hardened runtime builder.
- 1.0.0 — 2026-05-27 — Initial agent-skill/tool-SOP standard split from human Playbook/SOP creator. Why: review against Anthropic Agent Skills / Claude Code Skills and OpenAI GPT-5 / Agents guidance showed human-facing Playbooks/SOPs and agent-runtime skills needed separate standards.
- 1.1.11 — 2026-05-27 — Added post-upgrade re-score discipline to the create/draft procedure, eval cases, failure modes, and checklist. Why: during a workspace-hygiene hardening pass, the skill was scored before patching and then described as likely 24/26/hardened after edits without a formal post-patch re-score; future upgrade passes should either re-score or clearly label the readiness claim as an estimate/deferred verification.

## Source Lineage

Forked from `disciplined-hermes-playbook-sop-standard` on 2026-05-27 after review against Anthropic Agent Skills / Claude Code Skills and OpenAI GPT-5 / Agents guidance. The original standard was split into a human-facing Playbook/SOP creator and this agent-skill/tool-SOP builder.
