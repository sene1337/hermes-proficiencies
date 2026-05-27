# Pre-Publish Evidence Checklist

Use this checklist when `thorough-hermes-skill-publishing` is in publish-readiness review, safe sync, package/release hygiene, or public publish gate mode.

## 1. Artifact Pinning

Record:

- skill name;
- version;
- source path;
- runtime/private/public/pasted classification;
- support files included;
- intended destination and audience.

Do not review an ambiguous “the skill” without pinning the exact artifact.

## 2. Boundary Evidence

For any repo involved, capture:

```bash
pwd
git status --short
git remote -v
```

Confirm:

- private/runtime repo is not being pushed publicly;
- publish repo remote is the intended destination;
- there is no unreviewed dirty state that changes the publish artifact;
- the operation is happening in the intended path.

If path, repo, or remote is unclear, stop and ask.

## 3. Diff Evidence

Before sync/copy:

- inspect existing destination state;
- compare source and destination when both exist;
- identify exact files to copy/edit.

After sync/copy:

- run git diff/status in the destination repo;
- review every changed line for privacy, portability, and accidental regression;
- list files changed/copied/deleted in the final report.

Never blind rsync private/runtime trees into public repos.

## 4. Runtime / Validation Evidence

Capture one or more:

- live Hermes behavior evidence;
- validator/test command output;
- reproducible manual test steps;
- explicit deferral with reason and risk impact.

Publish readiness is blocked if the claimed behavior has not been proven and the skill relies on that behavior.

## 5. Package / Archive Evidence

For archives, packages, or release assets, inspect contents before upload:

```bash
tar -tf <archive>
unzip -l <archive>
```

Check for:

- `.git/` directories;
- staging wrappers that should not ship;
- temporary files;
- private notes/logs/memory files;
- generated files not intended for release.

## 6. Public Write Gate

Before `git push`, release creation, package upload, or public posting, present:

- exact repo/path/remote;
- exact command/action to run;
- evidence summary;
- unresolved risks;
- what will not be touched;
- approval required.

Do not execute public writes without explicit approval for the scoped action.
