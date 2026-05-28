# Destructive / Bulk Operation Mode

Use when a task might delete, move, rename, overwrite, bulk-sync, recursively modify, publish, or otherwise cause hard-to-reverse changes.

### 9. Destructive Operation Guardrails

- Never run rm -rf, bulk deletes, or dangerous overwrites on user data without explicit confirmation.
- Do not use broad permanent dangerous-command approvals for convenience. If an approval prompt offers an always/permanent option for broad patterns like `recursive delete`, prefer once/session unless the user explicitly asks for a durable allowlist. If a broad permanent allowlist is accidentally created, remove the specific config entry promptly and verify the parsed config value.
- Do not make the user choose between abstract cleanup strategies unless the tradeoff is genuinely strategic. Recommend the safest clean-final-state path, then ask only for the concrete approval required.
- For high-risk operations, describe the intended change and wait for approval.
- For mid-work delete/destructive approval prompts, include the reason directly in the approval ask box: why the deletion is needed, the exact path/scope, and what is explicitly not being touched. The reason must explain the operational/user benefit (for example, "remove stale runtime leftovers so the installed skill matches the source of truth"), not merely restate the shell operation (bad: "recursive delete"). Keep it short and decision-light.
- Balance both user concerns: avoid reckless destructive changes **and** avoid leaving stale copies, orphan files, or cleanup debt on disk for the user to review later. Recommend the clean final-state path yourself; do not make the user choose among abstract cleanup strategies unless there is a real strategic tradeoff.
- When using terminal for file operations, show the command first when it is destructive.
- For protected iCloud wiki paths, treat **any write operation** as high-risk, even if the change is small.

## Approval Format

Approval requests must include: short reason, exact paths/scope, operation, what is explicitly not touched, and rollback/safety plan when relevant.
