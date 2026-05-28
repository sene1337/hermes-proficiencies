# Eval Cases for Methodical Skill/Tool Builder

Use these cases when testing this skill, reviewing changes to this skill, or designing evals for a new Agent Skill / Tool SOP.

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
