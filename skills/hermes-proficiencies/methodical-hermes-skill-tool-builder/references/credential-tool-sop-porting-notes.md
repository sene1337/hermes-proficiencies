# Credential Tool SOP Porting Notes

Use these notes when converting a password-manager, secret-vault, sudo-access, API-key, or credential-handling SOP from another agent/workspace into a Hermes Tool SOP skill.

## Core Lesson

A credential SOP is rarely safe to port verbatim. Treat it as source material and extract a Hermes-native runtime contract.

Required conversion steps:

1. Separate portable behavior from private/local identifiers.
   - Portable: safe `op read` / vault lookup patterns, no-secret-output verification, approval thresholds, failure modes.
   - Private/local: vault IDs, item IDs, host names, service-account names, personal account labels, postmortem paths.

2. Merge the tool SOP with the companion secret-handling SOP.
   - A password-manager command list is incomplete without anti-leak rules.
   - Include “never print secrets,” “never write secrets to temp files,” “verify by length/hash/last-4,” and “suppress command output that can leak.”

3. Preserve service/gateway startup lessons as warnings, not blindly copied platform rules.
   - Example durable rule: do not wire secret fetches into long-running service startup unless that service environment is proven to carry required auth env vars and failure mode is safe.
   - Avoid copying OpenClaw-specific rules like `openclaw.json` or SecretRefs directly into Hermes unless explicitly adapting them.

4. Add Hermes runtime boundaries.
   - What Hermes may do autonomously: check CLI version, check token presence without printing it, verify vault access by exit code/count.
   - What requires approval: writing credentials to config, using sudo, changing gateway/service secrets, rotating credentials.
   - What is forbidden: printing full secrets, dumping item JSON, writing secrets to logs/temp files, using `launchctl print` on secret-bearing services.

5. Add eval cases.
   - Should trigger: user asks to retrieve/verify/use a secret from 1Password or another vault.
   - Should not trigger: generic config edit with no credential access.
   - Missing setup: CLI absent or auth env var missing.
   - Dangerous action: user asks to paste a full secret into chat or overwrite a service credential.
   - Gateway/service case: secret lookup in LaunchAgent/service startup.
   - Public publishing case: private vault/item IDs must be redacted or templated.

## Recommended Hermes Skill Shape

Private/local skill:
- May include actual local vault IDs and item IDs if operationally necessary.
- Must clearly mark them as private/local and not publication-safe.

Public/shareable skill:
- Use placeholders such as `<VAULT_ID>`, `<ITEM_ID>`, `<FIELD>`, `<HOST>`, `<SERVICE_ACCOUNT_NAME>`.
- Move any source-workspace incident details to a private reference file or summarize generically.

## Review Heuristic

If the SOP exposes how to access secrets but does not define how to avoid leaking them, score Tool/action safety no higher than 1/2.

If the SOP contains private vault/item IDs and does not mark them private or provide a redaction path, score Portability no higher than 1/2.
