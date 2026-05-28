# Skill Source / Runtime Hygiene Mode

Use when a task touches installed Hermes skills, private skill source repos, source/runtime sync, category placement, duplicate skill copies, or public-bound skill work.

### 2. Hermes Skill Source-of-Truth Rule

Treat installed Hermes skills in `~/.hermes/skills/` as the user's canonical **private runtime skill library** when they are actively worked on or generated/agent-created and tracked by git.

Default architecture for private/local skills:

```text
git-controlled ~/.hermes/skills/ runtime library
→ Hermes loads and validates the same files it edits
→ optional publish-clean export to ~/.hermes/skill-dev/ or a public/shared repo only after review
```

Required behavior:
- For active private/local skills, edit the installed runtime copy and use the `~/.hermes/skills/` git repo as the safety net.
- Track only skills the user actively works on plus generated/agent-created skills. Do not track hub-installed skills, archived/stale skills, curator metadata, lockfiles, or runtime noise by default.
- Use `~/.hermes/skill-dev/` only for skills intended for public/shared release, publish-clean export, or other packaging work outside the installed runtime library.
- Before skill edits, check `git status --short --branch` in `~/.hermes/skills/` and verify whether the target skill is tracked or intentionally ignored.
- After skill edits, review `git diff` in `~/.hermes/skills/` and commit durable private skill-library changes.
- Before any public GitHub push/publish, load and follow `thorough-hermes-skill-publishing`; never push the full private runtime skill library publicly.
- For ignored hub/bundled skills, do not patch them as durable local source unless the user explicitly decides to bring that skill into the tracked private runtime library.
- Use `tool skills` as the plain-language default for skills that teach Hermes a tool, CLI, API, platform, vault, account, or local workflow. Use `private/local tool skills` for tool skills bound to the user's vaults, accounts, machines, paths, and workflows. Use `Hermes proficiencies` for public/shareable behavior or attribute skills. Avoid `runtime skills` as a category name because all installed skills are runtime-loaded.
- Keep artifact type distinct from publication status: a private proficiency is still a proficiency; a private/local tool skill is still a tool skill; public-bound work requires export/review even if the working copy lives in runtime git.

### 3. Runtime Skill Category Selection Rule

Hermes runtime supports optional category folders under `~/.hermes/skills/`, and the system prompt derives a skill's category from its folder path. Category folders are not mere tags; they affect how the skill library is browsed, indexed, and mentally routed by future agents.

Before installing, moving, or syncing a skill into runtime, choose the category deliberately from the artifact's operating purpose, not from the current project, current conversation, implementation language, or where the work happened.

Category decision flow:

```text
Human-facing Playbook/SOP:
  usually not installed as a runtime skill unless Hermes is being taught to create/review that artifact type;
  use an intentional human-operations/docs/playbooks category only after a category decision.

Tool SOP Skill:
  place under the concrete tool/domain category (devops, productivity, note-taking, media, github, etc.);
  private/local-account-bound Tool SOPs should still use a runtime folder that describes the tool/domain.

Agent Skill serving a domain:
  place under the operating domain the behavior serves, not the source folder, current project, or authoring context.

Hermes Proficiency / broad agent attribute:
  place under `hermes-proficiencies` for now; this is the accepted temporary/local bucket for broad Hermes behaviors like tidy, thorough, methodical, and helpful.

Review Protocol:
  prefer a support file inside the governed skill; create a dedicated skill only if the protocol needs independent invocation across multiple artifact families.

If no existing category fits cleanly:
  pause and propose a category instead of defaulting to the nearest familiar bucket.
```

Do not use `software-development` as a catch-all just because the skill was authored while coding or editing Hermes. Skills such as `tidy-hermes-workspace-hygiene`, `methodical-hermes-skill-tool-builder`, and publishing/review proficiencies are not limited to software development; they need a category chosen from their reusable operating role.

When category placement is uncertain, use the user-built logic: classify the artifact by type and use-case first (Playbook, SOP, Tool SOP, Review Protocol, Tool Skill, Hermes Proficiency), then choose or create the runtime/source bucket.

Do not resolve import uncertainty by creating broad final buckets such as `misc`, `frameworks`, or generic `operations`. Stage unclear imports in the nearest honest existing domain, leave a taxonomy note, and revisit once enough source materials show the real cluster.

### 4. Private Runtime Git Repo Version-Control Rule

Use the private git repo at `~/.hermes/skills/` as the safety net for the user's active private/runtime skill library, but do not confuse private runtime history with publication safety.

Core rules:
- `~/.hermes/skills/` may be a git repo, but it should track only the skills the user works on plus generated/agent-created skills.
- Keep hub-installed skills, archived/stale skills, metadata like `.usage.json`, curator state, lockfiles, caches, and OS/editor noise untracked.
- `~/.hermes/skill-dev/` is reserved for public-bound skills, publish-clean exports, or packaging/release work; do not use it as a duplicate private source for every local skill.
- Before editing, check `git status --short --branch` from `~/.hermes/skills/`.
- No remote is safest for the private runtime repo. If a remote exists, verify it is private before any push.
- Never push the full runtime skill repo to a public remote; it can contain private/local procedures, paths, and history.
- Use `.gitignore` to prevent hub/runtime noise from being tracked, but remember that already-tracked files remain tracked until explicitly removed from git.

Recommended `.gitignore` baseline for the private runtime skill repo:

```gitignore
*
!.gitignore
!<tracked-category>/
!<tracked-category>/<tracked-skill>/
!<tracked-category>/<tracked-skill>/**
.usage.json
.usage.json.lock
.curator_state
.bundled_manifest
.DS_Store
*.tmp
*.bak
__pycache__/
*.py[cod]
```

Before any remote add or push:

```bash
git status --short --branch
git remote -v
git ls-files | grep -Ei '(secret|token|key|credential|password|\.env|\.pem|\.p12|chat_id|telegram|discord)' || true
```

If sensitive material was accidentally tracked, do not rely on `.gitignore`; stop and clean git history or create a fresh private repo before publishing.

## Detailed Regression Reference
