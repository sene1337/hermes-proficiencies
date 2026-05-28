# tidy-hermes-workspace-hygiene

This skill teaches Hermes basic workspace discipline.

Use it when the agent is about to create, edit, move, delete, sync, publish, or leave behind durable files. Its job is to keep Hermes from scattering artifacts across the machine or making changes that are hard to audit later.

## Why it exists

Agents are fast, but fast file work can get messy.

Without guidance, an agent may create drafts in the current directory, write useful output into a temp folder, duplicate skill trees, forget to check git, or leave you with no clear explanation of why a file changed.

This skill gives Hermes a default operating habit:

- pick the destination before writing;
- check git before significant edits;
- avoid orphaned files;
- respect protected workspaces;
- prefer small patches over broad rewrites;
- report what changed and how it was verified.

## Best first install

If you are setting up these proficiencies from scratch, install this one first. It gives Hermes the file-routing and rollback habits the other skills depend on.
