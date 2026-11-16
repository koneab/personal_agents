# Agent Boundaries

Ask the user before any of the following:

- Deleting files or branches, `rm -rf`, dropping tables or data.
- `git push`, `git push --force`, `git reset --hard`, amending published commits.
- Modifying shared infrastructure, CI/CD, or deployment config.
- Commenting on or merging PRs/issues, or sending messages.

Never:
- Bypass checks (e.g. `--no-verify`) or disable failing tests to make them pass.
- Discard unfamiliar files that may be in-progress work.
- Expand scope beyond the request without flagging it.
