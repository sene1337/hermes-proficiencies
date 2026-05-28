# Hermes Proficiencies

A small set of installable skills that teach Hermes better operating habits.

A fresh Hermes install can work, but it does not always know how you want work organized. If you let an agent run at full speed without guidance, it can scatter files across the hard drive, create duplicate folders, write drafts into temporary directories, forget why it made a change, or publish private runtime assumptions into a public repo.

These skills are meant to fix that baseline problem. They give Hermes a practical starting layer for workspace hygiene, skill creation, publishing safety, and human-readable playbooks/SOPs.

## Why I created this

When agents move quickly, the mess compounds quickly.

They create artifacts before deciding where those artifacts belong. They use whatever directory is convenient. They write into temp paths that may not survive a restart. Subagents sometimes ignore the structure the main agent was trying to follow. A few hours of high-volume work can leave you with redundant folders, untracked files, half-finished drafts, and no clean way to tell what changed or why.

That is annoying when you are experimenting. It is worse when you are building reusable skills, publishing to GitHub, or handing work to another person.

This repo is my attempt to give Hermes a better default operating system for that kind of work. Not a huge framework. Just the basic habits I kept needing:

- choose a real destination before creating files;
- initialize or respect git so changes are reversible;
- commit and log decisions in a way a human can audit later;
- keep private/local behavior separate from public/shareable artifacts;
- build skills using repeatable patterns instead of one-off prompts;
- write playbooks and SOPs that humans can actually follow.

The goal is simple: move fast without letting the agent turn your workspace into a junk drawer.

## What these skills cover

### `tidy-hermes-workspace-hygiene`

This is the "do not make a mess" skill.

It teaches Hermes to route files deliberately, check git before significant edits, avoid orphaned artifacts, respect protected paths, and leave behind enough evidence that you can see what happened. It is especially useful when an agent is creating lots of files, running subagents, editing skills, or working across multiple folders.

The practical benefit: less hard drive clutter, fewer mystery files, safer changes, and a real rollback path through git.

### `thorough-hermes-skill-publishing`

This is the public-publishing safety skill.

A skill can work perfectly on your machine and still be unsafe to share. It might contain local paths, private repo names, internal changelogs, account assumptions, credential references, or workflow details that do not belong in a public GitHub repo.

This skill gives Hermes a publishing checklist: validate the working skill, scan for private data, clean up support files, verify the target repo, disclose the GitHub auth source before any write, and treat public publishing as a separate approval gate.

The practical benefit: you can turn private skill work into a public repo without learning every leak and packaging mistake the hard way.

### `methodical-hermes-skill-tool-builder`

This is the skill-making skill.

It helps Hermes create better runtime skills for itself, including Tool SOP skills for CLIs, APIs, credential workflows, local tools, and recurring agent tasks. It pulls together the patterns that make skills useful in practice: clear invocation rules, runtime contracts, allowed and forbidden actions, stop/ask/escalate rules, eval cases, support files, and verification steps.

The practical benefit: when you ask Hermes to create or migrate a skill from another agent system, it has a structure to follow instead of inventing a format from scratch.

### `helpful-hermes-human-playbook-sop-creator`

This is the human playbook/SOP skill.

Use it when the output is meant for people, not just for Hermes. It helps create playbooks, SOPs, operating standards, and review protocols that a teammate can read and execute without needing the original chat context.

This one is optional. It should load when you specifically want Hermes to produce human-facing operating documents.

The practical benefit: better team docs, less hidden context, and more consistent human procedures.

## How the pieces fit together

These skills separate four jobs that agents often blur together:

- Workspace hygiene: where files go, how git is used, how changes stay reversible.
- Skill building: how Hermes learns a repeatable agent behavior or tool workflow.
- Publishing safety: how private working material becomes safe public material.
- Human playbooks/SOPs: how agent-assisted knowledge becomes something people can follow.

Keeping those jobs separate matters. A Tool SOP for an agent is not the same thing as a human SOP. A working private skill is not automatically publishable. A file created by an agent is not "organized" just because it exists somewhere on disk.

## Repository layout

```text
skills/hermes-proficiencies/<skill-name>/SKILL.md
skills/hermes-proficiencies/<skill-name>/README.md
skills/hermes-proficiencies/<skill-name>/references/...
skills/hermes-proficiencies/<skill-name>/templates/...
```

Each `SKILL.md` is the runtime file Hermes loads. The `README.md` files are for humans browsing the repo. Support files hold deeper checklists, templates, eval cases, and mode-specific procedures.

## Installation

Copy the skill directories into your Hermes skill library:

```bash
mkdir -p ~/.hermes/skills/hermes-proficiencies
cp -R skills/hermes-proficiencies/* ~/.hermes/skills/hermes-proficiencies/
```

Then restart Hermes or reload skills so the new skills are available.

## Suggested starting point

If you only install one skill first, start with:

```text
tidy-hermes-workspace-hygiene
```

That is the foundation. It reduces workspace mess and gives Hermes better habits before it starts creating more artifacts.

If you plan to publish skills publicly, add:

```text
thorough-hermes-skill-publishing
```

If you want Hermes to create or migrate reusable skills, add:

```text
methodical-hermes-skill-tool-builder
```

If you want human-readable team procedures, add:

```text
helpful-hermes-human-playbook-sop-creator
```

## Design principles

1. Runtime behavior matters more than nice prose. A good skill changes what Hermes does.
2. File routing should happen before writing, not after the mess exists.
3. Git is the default safety net for serious agent work.
4. Public publishing needs its own review gate.
5. Private/local tool knowledge and public/shareable guidance should not be mixed by accident.
6. Human SOPs and agent Tool SOPs need different formats because they have different operators.
7. Important skills should be reviewed and improved after real use.

## License

MIT.
