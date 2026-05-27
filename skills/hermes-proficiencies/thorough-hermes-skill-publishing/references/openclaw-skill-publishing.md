# OpenClaw Skill Publishing SOP (Reference)

**Source:** ~/.openclaw/workspace/ops/playbooks/skill-building/sops/skill-publishing.md

Key principles extracted for Hermes:

- Runtime validation must happen before extraction to a portable skill.
- "Live lane works" and "publish-clean artifact" are separate gates.
- Always diff before rsync when syncing from workspace to skill repo.
- Remove all machine-specific paths, chat IDs, usernames, and private references.
- Check packaged artifacts for .git/ leakage.
- Extensions must live in the canonical extensions directory, not inside the workspace.
- Strong pre-publish checklist focused on data leakage prevention.