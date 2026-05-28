# Support File Format and Progressive Disclosure Guide

Use this when designing or reviewing support files for Hermes skills. Keep routine instructions in `SKILL.md`; move bulky, rare, historical, templated, or deterministic detail here.

### Support File Format Selection

Choose support-file formats by operational purpose, not convenience:

- **Markdown (`.md`)** — narrative procedures, human/agent context, source-lineage notes, examples, and mode references. Use when prose and judgment are the value.
- **YAML (`.yaml`/`.yml`)** — structured configuration, mode maps, checklists, option sets, and values that humans should edit safely. Use when comments and readability matter.
- **JSONL (`.jsonl`)** — append-only ledgers for decisions, eval runs, review results, failure observations, and historical events. Use when preserving chronology matters and agents should add records without rewriting history.
- **Scripts (`scripts/`)** — deterministic validation, API calls, transforms, packaging, scoring helpers, and repeatable checks. Use when prose would create brittle manual execution.
- **Templates (`templates/`)** — copyable output shapes, score sheets, prompts, config starters, or request bodies. Use when the artifact should be reused but not treated as factual history.
- **Assets (`assets/`)** — images, diagrams, fixtures, screenshots, or binary examples that are required only in specific modes.


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
