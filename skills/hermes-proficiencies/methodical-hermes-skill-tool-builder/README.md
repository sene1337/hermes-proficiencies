# methodical-hermes-skill-tool-builder

This skill teaches Hermes how to create better skills for itself.

Use it when you want Hermes to turn a repeated workflow, tool procedure, agent behavior, or imported procedure from another agent system into a reusable Hermes skill.

## Why it exists

A useful skill is more than a saved prompt.

Hermes needs to know when to load it, what tools it may use, when to ask for approval, when to stop, what output shape to produce, and how to verify that the work was done correctly. Tool SOP skills need even more structure because they often involve credentials, local CLIs, APIs, services, or files.

This skill gives Hermes a repeatable framework for building those skills instead of inventing a new format every time.

## What it helps create

- Runtime Hermes skills for repeated agent behaviors.
- Tool SOP skills for CLIs, APIs, credential-backed tools, and local workflows.
- Score sheets and review loops for improving skills after real use.
- Support files, templates, eval cases, and verification checklists.

## When not to use it

Do not use this for human playbooks or SOPs unless the goal is to teach Hermes how to create or review those artifacts. For docs that humans will read and execute directly, use `helpful-hermes-human-playbook-sop-creator`.
