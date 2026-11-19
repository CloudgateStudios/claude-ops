# claude-ops

Shared automation that lets Claude pick up tickets across every CloudgateStudios repo.

- `.github/workflows/claude-agent.yml` — reusable workflow each repo calls (via its own `claude.yml`). Runs Claude Code when an issue gets the `claude` label or someone mentions `@claude`.
- `.github/workflows/board-dispatch.yml` — runs every 30 minutes against org project #1:
  - adds any open org issue not on the board to **Backlog**
  - **Ready for Agent** → labels the issue `claude` (starts Claude) and moves it to **In Progress**
  - **In Progress** with an open closing PR → moves it to **Needs Review**

Secrets (org level): `ANTHROPIC_API_KEY` or `CLAUDE_CODE_OAUTH_TOKEN`, and `CLAUDE_BOARD_TOKEN` (fine-grained PAT: Issues RW, Pull requests R, org Projects RW).
Optional org variables: `CLAUDE_PROJECT_NUMBER`, `CLAUDE_STATUS_NEW`, `CLAUDE_STATUS_READY`, `CLAUDE_STATUS_WORKING`, `CLAUDE_STATUS_REVIEW`.
