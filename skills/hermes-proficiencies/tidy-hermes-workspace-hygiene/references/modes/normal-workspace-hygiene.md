# Normal Workspace Hygiene Mode

Use when the task creates, edits, moves, routes, or verifies files inside an ordinary workspace or git repo.

## The Play

Use this operating sequence for any file-affecting task:

1. **Classify the workspace.** Identify the target path and whether it is a normal workspace, installed Hermes runtime state, private skill source repo, public publish repo, or protected iCloud wiki.
2. **Check safety state.** For normal workspaces and repos, check git root/status before edits. For protected paths, stop unless exact write scope was explicitly approved.
3. **Route before creating.** Decide the final path before writing. Do not create temporary-orphan files in the current working directory.
4. **Choose the least risky edit mode.** Prefer `patch` for existing files, `write_file` for new files or intentional complete rewrites, and terminal file operations only when they are the right tool.
5. **Verify with evidence.** Confirm paths, diffs/status, protected-path approval state, and absence of orphan files before reporting done.
6. **Feed learning back.** If the task exposes a new protected path, routing rule, naming exception, or failure mode, update this skill or its linked references.


## Decision Thresholds

Use these defaults when the user has not provided stronger instructions:

- **Significant change:** any edit outside a disposable temp directory that modifies existing user data, creates a durable artifact, touches more than one file, changes a protected/config/source-of-truth location, or would be annoying to reconstruct manually.
- **Non-trivial git change:** any code/config/skill/doc change intended to persist beyond the current session, any multi-file change, or any change that affects a source-of-truth repo.
- **Dangerous overwrite:** any full-file rewrite of an existing file, bulk copy/sync, move/rename/delete, generated output over an existing artifact, or command that can recursively affect directories.
- **Established workspace:** a directory with git, AGENTS.md/CLAUDE.md/HERMES.md, existing memory/docs/ops structure, README/conventions, or prior user-stated routing rules.

Default actions:

```text
If path is protected iCloud wiki:
  read/search/summarize only unless exact write scope is approved.

If path is ~/.hermes/skills and skill is shareable/important:
  treat as runtime copy; reconcile back to the correct source repo by skill type: proficiencies repo for Hermes proficiencies, soulbound repo for soulbound/tool skills.

If path is not git-controlled and change is significant:
  flag the lack of git/checkpoint safety and ask before proceeding.

If existing file needs a small edit:
  use patch, then verify diff/content.

If creating a durable artifact:
  choose final path first and include origin/changelog unless exempt.
```


### 1. Git Awareness (Mandatory First Step)

Before making changes in any directory:
- Check if the directory is inside a git repository.
- Prefer working inside git repos when possible.
- For non-trivial changes, consider creating a branch or making a commit before proceeding.
- When editing existing files in a git repo, prefer patch over full write_file rewrites.

Rule: If the target directory is not a git repo and the change is significant, flag this and ask whether to proceed or initialize git first.

### 6. File Routing Discipline

Do not default to the current working directory (~/.hermes/hermes-agent).

When the user has an established workspace structure, route new files according to the three-tier model:

```
memory/  — What happened (logs, task state, lessons, daily records)
docs/    — What we know (research, projects, deliverables, content)
ops/     — How we work (playbooks, SOPs, decisions, continuous improvement)
```

**Immediate Routing Rule:** Every file must be placed in its final (or clearly temporary) location in the same step it is created. Never create then "organize later."

**Detailed Routing Rules**

| Type of Output                        | Destination                                      |
|---------------------------------------|--------------------------------------------------|
| Research / analysis                   | docs/research/ or docs/projects/<project>/       |
| Project documents                     | docs/projects/<project-name>/                    |
| Deliverables for user (HTML, PDF)     | docs/deliverables/ or alongside source           |
| Daily logs / task state               | Use Hermes memory tool + todo tool               |
| Playbooks / SOPs                      | ops/playbooks/<category>/                        |
| Decisions / continuous improvement    | ops/decisions/ or ops/continuous-improvement/    |
| Temporary / scratch work              | Explicitly mark as temporary and clean up        |
| Utility scripts                       | scripts/ or project-local folder                 |
| Drafts / WIP                          | docs/drafts/ (with 7-day graduation rule)        |

### 7. Naming Conventions

- Use lowercase with hyphens: weekly-planning.md (not WeeklyPlanning.md)
- Be descriptive: delegation-checklist.md (not dc-v2.md)
- No dates in filenames unless it is a log or archive
- No banned suffixes: never use -v2, -final, -improved, -new (use git history instead)
- Drafts in docs/drafts/ may temporarily use version suffixes while iterating

### 8. New Standalone Files

New standalone files (playbooks, SOPs, research docs, trackers, etc.) should include:
- An origin block at the top stating when it was created, who made it, and why
- A Changelog section at the bottom with a v1.0 entry

Daily logs and temporary files are exempt from this requirement.

### 10. Hermes Tool Preferences

- Use the native memory tool for durable facts and task state instead of creating active-tasks.md files.
- Use the todo tool for task tracking.
- Use session_search when needing historical context instead of relying on scattered log files.
- Still respect the user's filesystem structure when they explicitly want files in docs/, ops/, etc.

### 11. Reference Existing Work

The following documents are considered authoritative until superseded:
- references/workspace-organization-reference.md
- references/file-routing-reference.md

When in doubt, follow the spirit of those documents.

## Verification

Use the shared verification checklist in `templates/workspace-verification-checklist.md`.
