# Workflow: Spec-Driven Development

- Every project uses OpenSpec, managed with Claude Code: `openspec init --tools claude`.
- Spec before code: do not create service folders or write code before there is a proposal for it.
- Flow: explore (think it through) → propose (proposal, specs, design, tasks) → apply (implement) → archive (merge into specs).
- On archive, always sync the change's delta specs into the main specs; do not ask whether to sync. Stop and ask only when a capability cannot be synced (for example, a MODIFIED requirement with no main spec).
- Keep each change small: one service or one feature per proposal.
- Constraints the assistant cannot infer from the code (naming, stack, repo layout, database decisions, scope) go in the project's `openspec/config.yaml` under `context`.

## Multi-repo projects

- A project with several repos keeps them side by side in one local folder named after the project (for example `~/Desktop/XBank/`).
- A central `<project>-specs` repo in that folder holds OpenSpec for the whole project: specs, changes, and `config.yaml` for every repo.
- Code repos hold code only. Changes are proposed and archived in `<project>-specs`; `apply` writes code into the target repo.
- After `apply`, I review the code repo's changes; after my approval it is committed (see [git.md](git.md)).
- `<project>-specs` is committed only once per change, after `archive`. Propose, apply, and archive edits to it stay uncommitted until then.
