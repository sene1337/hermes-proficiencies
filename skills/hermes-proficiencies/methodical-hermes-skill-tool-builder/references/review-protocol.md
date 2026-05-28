# Agent Skill / Tool SOP Review Protocol

Use this when the user asks to score, harden, review, or approve an Agent Skill, Tool SOP Skill, Review Protocol, or publishing-ready skill artifact.

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
- Maintainability: change-history entries explain what changed, why it changed, and cite reference links/paths/session context when available; related skills, support files, failure modes, and post-use audit support updates.
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

Root-standard exception: this standard itself should receive direct owner review before being treated as fully authoritative, because it governs the review loop and can otherwise grade its own logic. In the user's private skill library, the user is the root-standard reviewer.

### 8. Locked Evaluator / Anti-Gaming Rule

Do not let the same edit both weaken the scoring standard and pass because of the weakened standard. When a change modifies a rubric, score band, evaluator instruction, required eval case, or approval threshold:

1. Pin the pre-change evaluator text before editing.
2. State whether the change strengthens, clarifies, narrows, or weakens the standard.
3. Review the artifact against the pre-change standard first unless the user explicitly approves changing the standard before scoring.
4. If the standard must change, run a second review against the new standard and disclose both results or the reason the old score is obsolete.
5. Do not remove hard cases, dangerous-action evals, counter-triggers, or verification requirements merely to make a skill pass.
6. For root standards, request the user's review for material rubric changes before treating the updated standard as authoritative.

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
