# Git & PR Rules

- Keep PRs small and focused (target ~120 lines, one feature per PR)
- Always squash merge for clean linear history
- Commit often — at least once per feature completion
- Commit messages: imperative mood, describe why not what
- PR description must include: summary, test plan, screenshots if UI
- Never commit .env files or secrets
- Run `npm run lint && npm test` before every commit
