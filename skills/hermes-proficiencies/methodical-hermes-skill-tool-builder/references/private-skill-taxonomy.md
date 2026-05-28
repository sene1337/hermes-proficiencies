# Private Skill Taxonomy, Naming, and Attribution Hygiene

Use this when a skill's category, source repo, runtime placement, privacy boundary, attribution, or public-export wording is in question.

## the user's Skill Taxonomy

Use natural language first; thematic labels should clarify, not obscure.

```text
tool skills
  Plain-language default for skills that teach Hermes a tool, CLI, API,
  platform, vault, account, or local workflow.

soulbound skills
  Thematic/private subtype of tool skills: local/private skills bound to
  the user's vaults, accounts, machines, paths, and workflows. These belong
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

## Runtime Category Decision Flow

Classify the artifact by **operator + use-case** before choosing a runtime category. Do not invent vague final buckets just because several imports are still unclassified.

```text
Human-facing Playbook or SOP
  Primary operator: human.
  Runtime shape: usually not a Hermes skill unless Hermes is being taught to create/review that class of human artifact.
  Category: use a human-operations/docs/playbooks category only if that category exists intentionally; otherwise ask before creating one.

Agent Skill
  Primary operator: Hermes/agent.
  Runtime shape: behavior router + procedure + boundaries + verification.
  Category: choose the operating domain the behavior serves, not the source folder or authoring context.

Tool SOP Skill
  Primary operator: Hermes using a tool/API/CLI/platform/account.
  Runtime shape: exact do/don't/verify patterns, credentials/privacy/destructive/cost guardrails, and health checks.
  Category: put under the tool/domain category (`devops`, `productivity`, `note-taking`, `media`, `github`, etc.). If private/local-account-bound, it may also be called soulbound, but the runtime folder should still describe the tool/domain.

Hermes Proficiency
  Primary operator: Hermes applying a reusable attribute or operating discipline across domains.
  Runtime shape: compact behavior standard, mode router, and support files.
  Category: `hermes-proficiencies` is the accepted temporary/local bucket for broad agent-behavior attributes until a better public taxonomy exists.

Review Protocol
  Primary operator: Hermes or a human reviewer applying a scoring/control loop.
  Runtime shape: usually a section/support file inside the governed skill. Create a dedicated skill only when the protocol is reusable across multiple artifact families or needs independent invocation.
  Category: colocate with the governed domain unless it is a broad Hermes proficiency.
```

### Import / Placement Rules

- Preserve Playbook/SOP layering: posture and routing in the skill/playbook layer; exact SOPs in focused support files; simple Tool SOPs stay compact.
- Do not promote every Playbook, SOP, or Review Protocol into a top-level skill. Promote only when Hermes needs to invoke the behavior independently.
- Keep privacy level separate from artifact class: private proficiencies remain proficiencies; private tool/account skills remain tool skills; public-bound copies need publishing review regardless of category.
- If a source import exposes repeated but unclear classes, stage them in the nearest honest existing domain and leave a taxonomy note rather than creating broad final categories like `frameworks`, `misc`, or `operations` without user approval.
- For imported local/private materials, strip source-system branding from active runtime wording and describe the artifact in Hermes-native terms.

## Naming and Attribution Hygiene

When adapting user-built procedures into Hermes skills, keep active runtime skill language Hermes-native and neutral:

- Do not attribute the user's methods to a prior/source system brand in `SKILL.md`, filenames, support-file titles, or changelog entries.
- Do not use the user's personal name in active skill instructions, changelogs, or private-policy descriptions unless the user explicitly asks for a named biographical/profile artifact.
- Use neutral wording such as `the user`, `user-built`, `source materials`, `private source path`, `local/private policy`, or `external workspace`.
- Keep exact private source paths, if needed at all, inside deep private references and prefer placeholders like `<private source path>` for reusable skill guidance.
- Public/exportable skills must remove personal names, private source-system names, private paths, chat IDs, repo names, and local architecture assumptions unless the artifact is explicitly private and non-portable.

This is not cosmetic. Naming and attribution shape future agent reasoning: if a skill says a method came from another system or names the user unnecessarily, future sessions can misattribute ownership, leak private context, or make portable guidance look local-only.
