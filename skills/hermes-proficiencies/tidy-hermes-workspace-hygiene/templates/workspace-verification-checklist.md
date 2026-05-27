# Workspace Verification Checklist

After any file operation, confirm with evidence:
- [ ] Target path(s): list exact files/directories touched.
- [ ] Workspace classification: normal workspace, soulbound source repo, runtime skill copy, public publish repo, protected wiki, or temp.
- [ ] Git root/status: report git root and `git status --short --branch`, or state no git repo exists.
- [ ] Safety decision: branch/commit/checkpoint/approval decision and reason.
- [ ] Edit method: patch/write_file/terminal operation and why it was appropriate.
- [ ] File routing: final location chosen before creation; no durable files left in cwd or temp by accident.
- [ ] Existing-file edits: diff/content inspected after edit.
- [ ] Protected paths: private knowledge-base wiki work was read-only or explicitly approved for exact paths/operations.
- [ ] Runtime skills: if `~/.hermes/skills/` was edited for a serious/shareable skill, reconciliation to the correct proficiencies or soulbound source repo is queued or completed.
- [ ] Runtime category placement: installed skill category was chosen from artifact type/use-case, not from current project or authoring context; broad Hermes proficiencies are not defaulted into `software-development`.
- [ ] Private proficiencies source layout: skill directories live flat at `<PUBLISH_WORKSPACE>/<skill-name>/`, without redundant `skills/` or category wrapper folders.
- [ ] Skill-dev source placement: for Hermes proficiencies vs soulbound/tool skills, confirm the artifact lives in exactly one correct source repo and is not duplicated across sibling skill-dev repos.
- [ ] Private source layout: confirm source repo layout follows repo purpose. For `hermes-proficiencies`, skills live directly at repo root (`<skill-name>/`), not under `skills/` or `software-development/` wrappers.
- [ ] Subagents: if delegated, their context included allowed paths, output path, protected-path rules, and write permissions.
- [ ] Parent feedback: any new routing rule, protected path, naming exception, or failure mode was added to this skill or linked references.
