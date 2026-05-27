# Sensitive-Data Incident Rollback Mode

Use this mode when private data, credentials, chat IDs, personal files, or local-only architecture may have reached a shared/public repo, package, release, or message.

## Immediate Goals

1. Stop further publishing or syncing.
2. Pin what leaked and where it went.
3. Contain public exposure as fast as safely possible.
4. Rotate credentials if secrets may be exposed.
5. Preserve enough evidence for the owner without spreading the secret further.

## Procedure

### 1. Pin the incident

Record privately in the session/report:

- artifact/repo/package/message;
- public/shared destination;
- suspected leaked material category;
- commit/release/package/message identifier if known;
- whether credentials may be involved.

Do not paste full secrets back into chat.

### 2. Stop the line

- Do not continue publishing.
- Do not sync additional files.
- Do not create new packages from the contaminated tree.

### 3. Choose containment path

Prefer least-destructive containment first when it is enough:

- remove the public artifact/release if supported;
- revert the leaking commit and push the revert;
- replace package/release asset with clean version after approval.

Use destructive history rewrite only when necessary:

- `git reset --hard`;
- force-push;
- BFG/filter-repo history removal;
- release deletion.

These require explicit owner approval with exact repo, branch/tag/release, and consequence scope.

### 4. Rotate secrets

If credentials, tokens, private keys, passwords, cookies, or webhook URLs were exposed:

- treat them as compromised;
- revoke/rotate immediately;
- verify old credential no longer works;
- do not rely on git history cleanup as sufficient.

### 5. Verify clean state

After remediation:

- scan current tree/package;
- verify public artifact no longer contains the material;
- check git status/diff/remote;
- report what remains cached or outside direct control.

### 6. Private logging

Only if the user's private workflow authorizes it, write a private incident note with redacted details, remediation actions, and remaining risk. Never include incident logs in public artifacts.
