---
name: helpful-hermes-human-playbook-sop-creator
description: Use when creating, converting, or reviewing human-facing playbooks, SOPs, operating standards, or review protocols. Teaches Hermes to turn messy context into clear, repeatable artifacts a human can follow.
version: 1.1.3
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [proficiency, helpful, human-facing, playbooks, sops, review, operations]
    related_skills: [hermes-agent-skill-authoring, tidy-hermes-workspace-hygiene, thorough-hermes-skill-publishing, methodical-hermes-skill-tool-builder]
---

# Helpful Hermes Human Playbook/SOP Creator

## Purpose

Teach Hermes how to create, convert, and score **human-facing** operational artifacts:

- **Playbooks** — human-friendly operating doctrine for a recurring domain, role, cadence, or strategic workflow.
- **Standard SOPs** — exact, repeatable procedures a human can follow to complete a known task.
- **Review protocols** — strict scoring loops that make playbooks and SOPs clearer, safer, and more maintainable before humans rely on them.

This skill is deliberately optimized for artifacts that help humans act. It should produce documents that a new teammate, the future user, or post-compaction agent can hand to a human operator without needing the original conversation.

The user-built source structure is intentional: lightweight enough to ship fast, strict enough that operating knowledge survives compaction, delegation, reviewer drift, and human memory loss. Do not over-sanitize it into generic documentation advice.

For agent-runtime skills, tool SOPs, progressive-disclosure design, tool permissions, eval cases, and stop/ask/escalate behavior, use `methodical-hermes-skill-tool-builder` instead.

## When to Use

Use this skill when:

- The user asks for a playbook, SOP, operating standard, protocol, checklist, or repeatable workflow meant for humans.
- Existing notes, transcripts, user-built source artifacts, wiki material, or chat context need to become a clean human-followable operating artifact.
- A human team needs day-one-ready instructions, principles, cadence, quality checks, or a review rubric.
- A draft human-facing playbook or SOP needs to be scored for clarity, completeness, safety, and maintainability.

Do not use this for:

- Agent-native skill/tool SOP creation by itself; use `methodical-hermes-skill-tool-builder`.
- One-off answers that do not create durable operating knowledge.
- Public publishing checks by themselves; load `thorough-hermes-skill-publishing` for private-to-public release safety.
- File movement or workspace cleanup by itself; use `tidy-hermes-workspace-hygiene`. If creating/saving a playbook, SOP, template, or review artifact as a file, load tidy in addition because Hermes is about to create durable files.

## North Star Principles

1. **Day One Ready.** Any new human or post-compaction agent can pick up the playbook/SOP and execute on day one with zero author handholding.

2. **Learn Once, Capture Forever.** A wise person learns from the mistakes of others; a fool learns only from their own. Every process worth repeating gets captured so the lesson survives the session where it was learned.

3. **Ship Fast, Polish Deliberately.** Documentation should accelerate velocity, not kill it. Rapid capture and iterative polish beat perfectionism and heavy process.

4. **Inspection Is the Standard.** A playbook that is not reviewed on cadence is a wish, not an operating standard. Nobody respects what you do not inspect; inspect what you expect.

5. **Why Before How.** Playbooks explain purpose, principles, and operating rhythm. SOPs explain exact steps. When a playbook tries to do both, split it.

6. **Human UX Matters.** Favor clear headings, short sections, copyable templates, decision trees, named frameworks, and checklists over dense theory.

7. **No Context Debt.** The artifact should not depend on hidden chat history, author memory, or vague tribal knowledge.

## Artifact Type Decision

Pick the artifact type before writing.

```text
If the artifact explains a domain, role, cadence, principles, operating rhythm, or strategic workflow:
  Build a Playbook.

If the artifact gives exact repeatable steps for a known human task:
  Build a Standard SOP.

If the artifact mainly defines quality gates, scoring rubrics, adversarial review, or approval loops:
  Build a Review Protocol, or a Review section inside the parent playbook/SOP.

If the artifact teaches an AI agent how to use tools, route skill invocation, manage runtime behavior, or execute under tool permissions:
  Use methodical-hermes-skill-tool-builder instead. Tool SOPs are mainly agent-facing, even when they borrow SOP formatting.

If the artifact is itself a standard for creating/scoring Playbook/SOP/Tool-SOP skills:
  Treat it as a class-level meta-skill. Keep human-facing standards here and agent-runtime/tool standards in methodical-hermes-skill-tool-builder; link them rather than blending them.

If the artifact is tiny, time-sensitive, mechanical, or still in discovery:
  Build a Lightweight SOP Draft, mark it provisional, and do not use it for high-stakes work.
```

## Playbooks, SOPs, and Skills Relationship

Treat Playbooks, SOPs, Tool SOPs, and Review Protocols as **skill-shaped operating artifacts** with different primary operators:

- Human Playbooks and Human SOPs are repeatable skill formats optimized for human comprehension, accountability, and execution.
- Tool SOPs are mainly for agents: they teach Hermes how to use a tool, API, CLI, repo, account, browser flow, or platform safely under runtime constraints.
- Review Protocols are scoring/control-loop skills: they define how artifacts are judged, fixed, and re-scored.
- A “skill that teaches Hermes to create Playbook/SOP/Review Protocol skills” is a meta-skill/class-level builder task. Route human-facing artifact standards here, and route agent-runtime Tool SOP / skill-builder standards to `methodical-hermes-skill-tool-builder`.

Do not collapse these into one generic “documentation skill.” The reusable insight is the shared skill-shaped structure; the operational split is the intended operator and runtime behavior.

## Human Playbook Standard

Use this for operating domains and repeatable strategic workflows.

Playbooks say **what**, **when**, and **why**. SOPs say **how, exactly**.

### Required Shape

```markdown
---
name: <artifact-name>
description: Use when <human-facing trigger>. <operating behavior this playbook supports>.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [playbook, human-facing, <domain>]
    related_skills: [<related-skills>]
---

# <Playbook Title>

**Objective:** One sentence. What does this playbook achieve?
**Owner:** Who maintains and improves it.
**Executor:** Optional. Who runs the process and reports gaps. Skip if Owner is also Executor.
**Reviewer:** Who inspects outcomes. Usually the user for important operating standards.
**Review:** Review frequency. Quarterly minimum for important playbooks.

---

## Purpose

One or two paragraphs explaining what outcome this playbook creates and why it matters.

## When to Use

- Trigger conditions
- Counter-triggers / when not to use

## Audience / Operator

Who the playbook is for and what baseline knowledge/access they need.

## North Star Principles

3-5 stable principles that should survive process changes.

For v1.0, principles may be marked `TBD — refine after first 3 executions` when domain understanding is still forming. Do not invent fake principles just to look complete.

## The Play

The core operating model. Choose the structure that fits:

- Cadence-based: Daily → Weekly → Monthly → Quarterly → Annual
- Flow-based: Stage 1 → Stage 2 → Stage 3 → Close
- Framework-based: If X → do Y; named decision tools; branching rules

This is where scripts, templates, checklists, and named frameworks live. If the executor cannot copy/paste something or directly follow a concrete artifact, the playbook is incomplete.

## Failure Modes

- **Failure:** What goes wrong
  **Fix:** What to do instead

## Linked SOPs / Templates

- SOPs, checklists, scripts, or templates that support the playbook
- Write `None yet` if none exist

## Change History


- 1.0 — YYYY-MM-DD — Initial release.
```

### Roles

Use three roles max:

- **Owner** — maintains the playbook and improves it.
- **Executor** — optional; runs the process and reports gaps. Skip if Owner is also Executor.
- **Reviewer** — inspects outcomes. This is the “inspect what you expect” role.

Avoid role sprawl. If a responsibility does not change how the artifact is maintained, executed, or inspected, do not add another role.

### Playbook Quality Bar

A human-facing Playbook is not done until:

- [ ] The objective is clear enough to judge success.
- [ ] Owner, optional Executor, Reviewer, and Review cadence are explicit.
- [ ] The intended human audience/operator is named.
- [ ] The principles explain the why, not just the steps.
- [ ] The Play contains enough concrete mechanics to act on.
- [ ] At least one copyable/followable artifact exists when the domain requires one: checklist, template, script, decision tree, or named framework.
- [ ] Supporting SOPs/templates are listed or explicitly absent.
- [ ] At least 3 practical failure modes are included.
- [ ] Review cadence is explicit and realistic.
- [ ] Change history is append-only and stored in the right place for the artifact type.
- [ ] The artifact is not a raw transcript or unprocessed external doc dump.

## Standard Human SOP Standard

Use this for exact repeatable procedures performed by humans.

### Required Shape

```markdown
---
name: <artifact-name>
description: Use when <human-facing trigger>. <procedure this SOP guides>.
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [sop, procedure, human-facing]
    related_skills: [<parent-playbook-or-related-skill>]
---

# <SOP Title>

**Objective:** One sentence. What does this SOP achieve?
**Prerequisites:** What the operator needs before starting.
**Owner:** Who maintains it.
**Operator:** Who performs it and what baseline competence is assumed.

---

## Procedure

1. Step one.
2. Step two.
3. Step three.

## Templates / Scripts / Checklists

Copy-paste artifacts this SOP produces or uses. Omit only if genuinely none.

## Quality Check

- [ ] A new operator can execute without asking the author questions.
- [ ] Preconditions and approvals are explicit.
- [ ] Outputs and verification are explicit.
- [ ] Parent playbook or related artifact is updated if needed.

## Change History


- 1.0 — YYYY-MM-DD — Initial release. <Context for why it earned an SOP.>
```

### SOP Creation Procedure

1. **Identify the source.** Where is the knowledge coming from?

   ```text
   Capture Method:
     The operator already does the process but keeps forgetting or repeating explanation.
     Document what exists before it is forgotten again.

   Interview Method:
     Someone else knows how.
     Interview them, explore the real state, then document the procedure.

   Camcorder / Black Box Method:
     Nobody has done it cleanly yet.
     Do it once, record every step, then extract the SOP from the recording/log.
     For screen workflows: QuickTime screen recording → transcript/notes → step extraction.
   ```

2. **Explore before writing.** Inspect the actual files, tools, commands, state, people, approvals, and constraints when relevant. Do not infer the workflow from its name. The “inbox” might be files, email, a database, or a physical tray. Assume nothing.

3. **Identify the operator.** Specify who will perform the procedure and what they must already know or have access to.

4. **Pick the template.** Playbook, Standard SOP, Review Protocol, or Lightweight SOP Draft.

5. **Draft for the general case.** Name for durable scope, not the current narrow incident. Pressure-test: would this name still work if the tool changed, the team doubled, or the use case expanded?

6. **Keep the structure tight.** Default to the defined sections. If something does not fit, add it only when necessary, flag it in review notes, explain why the template needs to evolve, and log the change in the artifact's change history.

7. **Make it human-operable.** Use concrete steps, decision points, expected outputs, examples, templates, and checklists. If the operator cannot copy/paste or directly follow something concrete, the SOP is probably still too theoretical.

8. **Review.** Run the Human Playbook/SOP Review Protocol below. For lightweight SOPs, the quick self-check is enough for v1.0, but schedule full polish.

9. **Link and checkpoint.** If the artifact will be saved to disk, load `tidy-hermes-workspace-hygiene` before writing so Hermes routes it correctly and does not create orphan files. Link from the parent playbook’s Linked SOPs/Templates section. If the artifact lives in a git-controlled workspace, commit the parent + child updates together after validation.

10. **Feed back.** Did you learn a new pattern, failure mode, or quality bar during this build? Update the parent playbook, not just the SOP. Learnings in the parent help every future SOP. If nothing new was learned, skip this step.

## Lightweight SOP Drafts

Use only when the process is small, low-risk, mechanical, time-sensitive, or still in discovery.

### Required Shape

```markdown
# <SOP Title>

**Objective:** One sentence.
**Owner:** Who maintains it.
**Operator:** Who performs it.
[ ] Provisional / Polish Later

---

## Procedure

1. Step one.
2. Step two.

## Gotchas

- What to watch for.

## Change History

- 1.0 — YYYY-MM-DD — Created fast-track. <Context>.
```

### Lightweight Rules

- Skip full adversarial review only for v1.0; use quick self-check + notify reviewer instead.
- Must still include Gotchas.
- Schedule full polish + adversarial review within 7 days.
- If it grows in complexity, run the full Review Protocol immediately.
- Do not use for critical, high-stakes, external-facing, financial, legal, safety, publishing, credential, destructive, or irreversible operations.

## Human Playbook/SOP Review Protocol

Run this before trusting an important human-facing Playbook, SOP, or Review Protocol.

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
What was built: Human Playbook
Score against: Human Playbook Standard

What was built: Human SOP
Score against: Standard Human SOP Standard + parent Playbook if present

What was built: Lightweight SOP
Score against: Lightweight rules + quick self-check; schedule full review within 7 days

What was built: Review Protocol
Score against: Review Protocol clarity + relevant parent standard

What was built: Agent skill or Tool SOP
Stop and switch to methodical-hermes-skill-tool-builder

What was built: Publishing-ready public artifact
Score against: this standard + thorough-hermes-skill-publishing
```

### 2. Quick Self-Check Before Full Review

Run this before spawning adversarial review.

**Standard SOP:**

- [ ] Header includes Objective, Prerequisites, Owner, and Operator.
- [ ] Procedure has numbered steps a stranger could follow.
- [ ] Templates/Scripts/Checklists included when applicable.
- [ ] Quality Check has concrete verification items.
- [ ] Change history exists and is append-only.

**Playbook:**

- [ ] Header includes Objective, Owner, Reviewer, and Review cadence.
- [ ] Principles are present or explicitly marked `TBD — refine after first 3 executions`.
- [ ] The Play is cadence-based, flow-based, or framework-based.
- [ ] Failure Modes has at least 3 entries.
- [ ] Linked SOPs/Templates section is present, even if `None yet`.

**Both:**

- [ ] Name survives scope expansion.
- [ ] No extra sections unless flagged for reviewer.
- [ ] Version starts at 1.0 for a new artifact.
- [ ] The artifact is not dependent on hidden chat context.

### 3. Run Adversarial Review

For agents, spawn a subagent or run an isolated review pass with only:

- the draft artifact
- the relevant standard
- the exact scoring instructions

Reviewer instruction:

```text
Score every section strictly. Flag exact violations with quotes. Do not be nice. Identify missing prerequisites, unclear steps, unsafe assumptions, non-portable details, hidden context, structure drift, weak owner/reviewer accountability, and places where a new human operator would get stuck.
```

For humans, paste the draft and standard into an LLM with the same instruction.

### 4. Score the Artifact

Use a 0-2 scale per category:

```text
0 = Missing or unsafe
1 = Present but vague, incomplete, or fragile
2 = Complete, clear, executable, and maintainable
```

Core categories:

- Trigger clarity: When to use / not use is obvious.
- Objective clarity: Success can be judged.
- Audience/operator clarity: The human user and assumed baseline are explicit.
- Owner/reviewer accountability: Owner, Reviewer, review cadence, and escalation/provisional path are explicit where needed.
- Structure compliance: Uses the correct artifact shape; any extra sections are justified and flagged.
- Human executability: A new human operator can follow it without hidden context.
- Copy-paste concreteness: The artifact includes concrete templates, checklists, scripts, decision trees, examples, or named frameworks when needed.
- Decision support: Branches, judgment calls, and edge cases are explicit enough.
- Verification: Quality checks prove the result.
- Safety: Side effects, privacy, credentials, destructive steps, and publishing risks are guarded.
- Portability: No accidental private paths, IDs, user-specific assumptions, or local-only references unless explicitly marked private.
- Maintainability: Append-only changelog, owner/reviewer/cadence, related artifacts, and failure modes support future updates.
- Parent feedback: New learnings are fed back to parent playbooks or related SOPs.

Interpretation:

```text
22-26 = Excellent. Ready after final owner/reviewer approval.
17-21 = Usable draft. Fix flagged issues before relying on it.
11-16 = Weak. Needs structural rewrite.
0-10  = Not acceptable. Rebuild from source.
```

### 5. Fix and Re-score

- Fix every gap flagged by the review.
- Re-score after fixes; fixing one issue can break another.
- For important playbooks/SOPs, save the score sheet or append a score summary to durable review notes. Do not rely on chat history.
- If updating an SOP exposes a parent playbook gap, update and re-score the parent.

### 6. Reviewer Loop

1. Owner/agent produces draft.
2. Adversarial review flags issues.
3. Owner/agent fixes issues.
4. Reviewer inspects final version.
5. Repeat until approved or explicitly accepted as a lightweight/provisional draft.

If the reviewer misses two consecutive reviews, the Owner escalates, names the blocker, or marks the artifact abandoned/provisional. Review cadence is mandatory, not aspirational.

Root-standard exception: this standard itself should receive direct human review from the user before being treated as fully authoritative, because it governs the review loop and can otherwise grade its own logic.

## Common Failure Modes

1. **All theory, no execution.** If the human cannot copy/paste or directly follow concrete steps, templates, scripts, checklists, examples, or decision frameworks, the artifact is incomplete.

2. **Principles without success.** Writing principles before defining the problem, outcome, and success criteria creates generic values sludge. Start with: what problem are we solving, what outcome are we after, what does success look like?

3. **Playbook bloat.** The Playbook says what and why. SOPs say exactly how. Split when the playbook turns into spaghetti.

4. **SOP without parent context.** A procedure with no linked playbook rots faster because nobody knows why it exists.

5. **Hidden operator assumptions.** If the SOP assumes access, vocabulary, authority, or prior context, name those assumptions in prerequisites.

6. **Workflow inferred from the name.** The “inbox” may not be email. Inspect the actual state before drafting.

7. **Over-narrow naming.** A name tied to a temporary tool, person, or incident will break when the process expands. Pressure-test the name against tool changes, team growth, and use-case expansion.

8. **Extra sections become format drift.** Default to the template. If a new section is necessary, flag it for reviewer and explain whether the template itself should evolve.

9. **Author grades their own work.** Use adversarial review. The creator is too close to the artifact.

10. **Learning stays local.** New failure modes discovered during creation must feed back into the parent playbook or related SOP.

11. **Reviewer becomes bottleneck or ghost.** If no review happens, mark the artifact provisional. If two consecutive reviews are missed, escalate or mark abandoned/provisional.

12. **Change history gets rewritten.** Change history is append-only. Do not hide why decisions changed.

13. **Process heaviness kills momentum.** Use lightweight drafts for low-risk early capture, then polish within 7 days.

14. **Agent-runtime concerns mixed into human docs.** Human docs should mention tools and scripts only as human-operable aids; agent invocation logic belongs in `methodical-hermes-skill-tool-builder`.

14a. **Shared skill shape mistaken for same artifact.** Playbooks, SOPs, Tool SOPs, and Review Protocols can all be skill-shaped repeatable formats, but they are not interchangeable. Classify by primary operator: human comprehension/execution belongs here; agent runtime/tool behavior belongs in `methodical-hermes-skill-tool-builder`; scoring/control loops should attach to the artifact class they govern.

15. **Private material leaks into public artifacts.** Load `thorough-hermes-skill-publishing` before any public repo sync.

## Verification Checklist

Before calling a human Playbook/SOP done:

- [ ] Correct artifact type selected.
- [ ] Human operator/audience is explicit.
- [ ] Objective and success condition are clear.
- [ ] Owner, Reviewer, and Review cadence are explicit where needed.
- [ ] Trigger and counter-trigger conditions are clear.
- [ ] Steps, cadence, or operating model are concrete enough to follow.
- [ ] Copyable/followable artifacts are included where needed: templates, scripts, checklists, decision trees, examples, or named frameworks.
- [ ] Branches, edge cases, and approval points are captured.
- [ ] Name survives scope expansion.
- [ ] Extra sections are absent or explicitly flagged/justified.
- [ ] Failure modes/gotchas are practical and specific.
- [ ] Change history exists and is append-only.
- [ ] Quality checks verify real outcomes.
- [ ] Score sheet or review summary is saved for important artifacts.
- [ ] Related parent playbooks or SOPs are updated.
- [ ] Adversarial review was run or explicitly deferred under lightweight rules.
- [ ] Score is acceptable for the risk level.
- [ ] Git-controlled artifacts are committed with parent/child changes together when appropriate.
- [ ] Public publishing checks are run separately before any public repo sync.

## Support Files

- `references/source-comparison-2026-05-27.md` — comparison of the original source Playbook Creation / SOP Creation / Review Protocol materials against this Hermes skill; records which source details were restored in v1.1.

## Source Lineage

Forked from `disciplined-hermes-playbook-sop-standard` on 2026-05-27 and deliberately narrowed to human-facing Playbook/SOP creation. Adapted from source Playbook Creation, SOP Creation, SOP Templates, and Review Protocol materials.
