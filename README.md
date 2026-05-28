# Hermes Proficiencies

Public, shareable **Hermes Agent proficiency skills**: class-level operating attributes that teach Hermes *how to work*, not just which tool to call.

These proficiencies are designed to keep an agent useful under real operating pressure: turning messy context into repeatable human playbooks/SOPs, building agent-runtime Tool SOP skills with guardrails, publishing skills without leaking private data, and enforcing workspace hygiene so the agent routes files deliberately instead of scattering drafts, temp files, duplicated skill copies, or destructive changes across the hard drive.

## Why these exist

These skills came out of a design problem: Playbooks, SOPs, Tool SOPs, Review Protocols, and Hermes Skills are all repeatable operating artifacts, but they serve different operators.

- **Human Playbooks/SOPs** need to be clear enough for a person to execute without hidden chat context.
- **Tool SOPs and Agent Skills** need runtime contracts: when to load, what tools are allowed, when to ask, when to stop, and how to verify.
- **Review Protocols** need scoring loops so artifacts can be judged, fixed, and re-scored instead of merely polished.
- **Publishing workflows** need a separate safety gate so local/private runtime behavior does not leak into public artifacts.

The goal of this repository is to make those distinctions explicit and reusable. These proficiencies are meant to be installed into Hermes so future sessions inherit the operating discipline: helpful human-facing artifact creation, methodical skill/tool-SOP construction, thorough publishing safety, and tidy workspace hygiene.

## Included proficiencies

- `helpful-hermes-human-playbook-sop-creator` — creates and scores human-facing Playbooks, SOPs, operating standards, and review protocols.
- `methodical-hermes-skill-tool-builder` — creates and scores agent-runtime Hermes Skills and Tool SOP skills with invocation contracts, guardrails, evals, and verification.
- `thorough-hermes-skill-publishing` — performs publish-readiness review, private-data scanning, package hygiene, and public-write gating for skills.
- `tidy-hermes-workspace-hygiene` — keeps agent file operations routed, git-aware, reversible, and respectful of protected/private workspaces.

## Repository layout

```text
skills/hermes-proficiencies/<skill-name>/SKILL.md
skills/hermes-proficiencies/<skill-name>/references/...
skills/hermes-proficiencies/<skill-name>/templates/...
```

## How to use

Copy the skill directories into your Hermes skill library, or adapt them into your own skill source repository. Before using them in a public/shared context, review and tune the protected-path, publishing, and approval policies for your environment.

## Design principles

1. **Runtime behavior beats documentation aesthetics.** A good skill changes what Hermes does: routes correctly, acts safely, stops when needed, and verifies outcomes.
2. **Progressive disclosure reduces context load.** Keep routing and common procedure in `SKILL.md`; put detailed modes, templates, and source-lineage notes in support files.
3. **Public publishing is a separate gate.** A skill can work locally and still be unsafe or too private to publish.
4. **Review loops prevent drift.** Important skills and SOPs should be scored, patched, and re-scored after real use.
5. **Human and agent artifacts differ.** Human SOPs optimize for human execution; Tool SOP skills optimize for agent runtime behavior under tool constraints.

## License

MIT.
