# Hermes Proficiencies

A small set of installable skills that teach Hermes better operating habits.

A fresh Hermes install can work, but it does not always know how you want work organized. If you let an agent run at full speed without guidance, it can scatter files across the hard drive, create duplicate folders, write drafts into temporary directories, forget why it made a change, or publish private runtime assumptions into a public repo.

These skills are meant to fix that baseline problem. They give Hermes a practical starting layer for workspace hygiene, skill creation, publishing safety, human-readable playbooks/SOPs, decision discipline, and continuous improvement.

## Why I created this

When agents move quickly, the mess compounds quickly.

They create artifacts before deciding where those artifacts belong. They use whatever directory is convenient. They write into temp paths that may not survive a restart. Subagents sometimes ignore the structure the main agent was trying to follow. A few hours of high-volume work can leave you with redundant folders, untracked files, half-finished drafts, and no clean way to tell what changed or why.

That is annoying when you are experimenting. It is worse when you are building reusable skills, publishing to GitHub, or handing work to another person.

This repo is my attempt to give Hermes a better default operating system for that kind of work. Not a huge framework. Just the basic habits I kept needing:

- choose a real destination before creating files;
- initialize or respect git so changes are reversible;
- own cleanup instead of turning the user into a git-status reporter;
- make small decisions without interrupting the user;
- bring real options and a recommendation when a decision is above the agent's authority;
- preserve the reason behind important decisions so they do not get reopened a week later;
- keep private/local behavior separate from public/shareable artifacts;
- build skills using repeatable patterns instead of one-off prompts;
- write playbooks and SOPs that humans can actually follow;
- run improvement loops that change behavior instead of creating process theater.

The goal is simple: move fast without letting the agent turn your workspace into a junk drawer.

## What these skills cover

### `tidy-hermes-workspace-hygiene`

This is the "do not make a mess" skill.

It teaches Hermes to route files deliberately, check git before significant edits, avoid orphaned artifacts, respect protected paths, and leave behind enough evidence that you can see what happened. It is especially useful when an agent is creating lots of files, running subagents, editing skills, or working across multiple folders.

The practical benefit: less hard drive clutter, fewer mystery files, safer changes, and a real rollback path through git.

### `decisive-hermes-decision-communication`

This is the decision-discipline skill.

It teaches Hermes to stop asking vague questions when it should be making a recommendation. The default pattern is 1-3-1: one clear problem, three real options, one recommendation. Hermes should use that thinking internally for small choices and act without bothering the user. For bigger choices, it should bring the user a real fork in the road, not a pile of half-formed questions.

It also helps preserve the reason behind decisions. That matters because humans forget too. A week later, someone should be able to ask "why did we choose this?" and get a useful answer instead of reopening the whole debate.

The practical benefit: fewer interruptions, better recommendations, and a decision record that keeps future work moving.

### `mindful-hermes-continuous-improvement`

This is the improvement-loop skill.

It came from a simple problem: agents can log mistakes forever without actually getting better. This skill keeps the loop honest:

```text
mistake -> root cause -> fix -> verify it stuck
```

It owns the recurring feedback loops around Hermes: regression capture, capability gaps, decision-miner review queues, file-janitor findings, cron health, and weekly review cards. It does not recreate things Hermes already does well, like session search, memory, skills, cron, or curator. It uses those native parts and adds inspection so they produce changed behavior.

The practical benefit: fewer repeated mistakes, better follow-through after corrections, and less process that exists only to make everyone feel organized.

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

These skills separate six jobs that agents often blur together:

- Workspace hygiene: where files go, how git is used, how changes stay reversible.
- Decision discipline: when Hermes should decide, when it should recommend, and how it preserves the reasoning.
- Continuous improvement: how mistakes become behavior changes instead of notes nobody reads.
- Skill building: how Hermes learns a repeatable agent behavior or tool workflow.
- Publishing safety: how private working material becomes safe public material.
- Human playbooks/SOPs: how agent-assisted knowledge becomes something people can follow.

Keeping those jobs separate matters. A Tool SOP for an agent is not the same thing as a human SOP. A working private skill is not automatically publishable. A file created by an agent is not "organized" just because it exists somewhere on disk. A decision-quality skill should not own every recurring review cron just because decisions are involved; continuous improvement owns the loop, while the decision skill owns the quality bar.

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

If you want Hermes to make clearer recommendations and preserve decision rationale, add:

```text
decisive-hermes-decision-communication
```

If you want Hermes to maintain improvement loops instead of repeating the same mistakes, add:

```text
mindful-hermes-continuous-improvement
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
7. Important decisions should carry enough rationale that a future human can understand why they were made.
8. Improvement loops should change behavior, not just create more records.
9. Important skills should be reviewed and improved after real use.

## License

MIT.
