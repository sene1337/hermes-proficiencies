# Private-Data Scan Checklist

Use this checklist before sharing, packaging, or publishing a Hermes skill.

## Scan Targets

Look for:

- local paths: `/Users/`, `/home/`, absolute project paths, private knowledge-base/wiki paths;
- profile-specific Hermes paths: memories, logs, private cron output, runtime-only assumptions;
- personal identifiers: names, family members, account handles, email addresses, phone numbers;
- chat/platform identifiers: Telegram/Discord IDs, topic IDs, webhook URLs;
- organization/private repo names not intended for publication;
- secrets: API keys, tokens, passwords, session cookies, bearer strings, private keys;
- vault/item names, 1Password references, sudo passwords, secret-manager paths;
- private data references: MEMORY.md, USER.md, daily logs, personal notes, meeting notes;
- examples that reveal private operating architecture rather than portable guidance.

## Suggested Read-Only Searches

Adapt patterns to the repo and avoid dumping suspected secrets into chat.

```bash
grep -RInE '(/Users/|/home/|\.hermes/(mem|memory|logs|cron|profiles)|Telegram|Discord|chat_id|thread_id|Bearer |api[_-]?key|password|BEGIN .*PRIVATE KEY)' .
```

Prefer counts, filenames, line numbers, hashes, or redacted snippets over printing secrets.

## Remediation Choices

For each finding, choose one:

- **Remove** if irrelevant to public use.
- **Parameterize** with placeholders like `<HERMES_HOME>`, `<YOUR_REPO>`, `<CHAT_ID>`.
- **Move to private reference** if it is useful only for the owner/local runtime.
- **Mark private-only** if the skill is intentionally not publishable.
- **Block publish** if a secret, credential, or sensitive personal detail is present.

## Public Artifact Rule

A public/shareable skill should not mention the owner, the local user, private repo names, chat IDs, profile-specific paths, daily logs, memory files, or local-machine architecture unless the entire artifact is intentionally labeled as local/private and is not being published.
