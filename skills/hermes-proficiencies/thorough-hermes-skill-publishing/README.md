# thorough-hermes-skill-publishing

This skill teaches Hermes how to prepare a private or local skill for public sharing.

A skill can be useful on your machine and still be unsafe to publish. It may include local paths, internal changelogs, account assumptions, private repo names, credential references, or instructions that only make sense in your environment.

## What it does

This skill adds a publishing gate before Hermes shares skill work publicly. It covers:

- validating the working skill before export;
- scanning for private data and machine-specific assumptions;
- removing internal changelogs and local-only support files;
- checking package and repo hygiene;
- verifying the target remote before a public write;
- disclosing the GitHub auth source before any push or API mutation;
- separating skill metadata author, git commit author, committer, and pusher account.

## When to use it

Use this before pushing, packaging, releasing, or sharing Hermes skills.

Do not use it as a general writing standard. Its job is narrower: keep private runtime work from leaking into public artifacts.

## Install path

Copy the whole folder into your Hermes skills directory, for example:

```bash
~/.hermes/skills/hermes-proficiencies/thorough-hermes-skill-publishing/
```

Then restart Hermes or reload skills.
