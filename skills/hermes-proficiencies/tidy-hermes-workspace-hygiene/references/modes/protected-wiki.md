# Protected Wiki Mode

Use when the task touches the user's iCloud wiki, Citadel wiki, personal knowledge base, or any protected knowledge base path.

### 5. Protected iCloud Wiki Rule

Treat iCloud wiki directories as protected knowledge bases, not ordinary workspaces.

Default stance:
- **Read-only by default.** Searching, reading, quoting, and summarizing are allowed when directly relevant.
- **No edits, deletes, moves, renames, rewrites, bulk formatting, cleanup, or file creation inside iCloud wiki paths** unless the user gives explicit, current-task permission for that exact scope.
- **No inferred permission.** A broad request like "work on my Citadel OS" or "clean up docs" does not authorize touching wiki files.
- **No subagent freelancing.** Delegated agents must be told the wiki is protected and must not modify it unless the delegation context includes the exact approved file paths and allowed operations.

Before any wiki write operation, stop and present:
1. The exact path(s) to be changed.
2. The exact operation: create, patch, rename, move, or delete.
3. The reason the wiki itself must be touched instead of using a draft/staging area.
4. The rollback/safety plan.

Only proceed after explicit approval.

## Escalation

Before any write, present exact paths, exact operation, why the protected wiki itself must be touched, and rollback/safety plan. Wait for explicit approval.
