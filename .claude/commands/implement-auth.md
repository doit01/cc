Implement the $ARGUMENTS feature for the auth module.

## Steps

1. Read the spec in `docs/specs/$ARGUMENTS.md`
2. Write failing unit tests first (TDD: red → green → refactor)
3. Implement following the architecture defined in CLAUDE.md
4. Write integration tests against a real PostgreSQL instance
5. Run full test suite: `npm test`
6. Run linter and fix any issues: `npm run lint`
7. Run build to verify type safety: `npm run build`

## Review

After implementation, use subagents to:
- **Security review**: check for token exposure, SQL injection, missing rate limiting
- **Code review**: verify architecture compliance, no `any` types, proper error handling

Do NOT create a PR until both reviews pass. Challenge the implementation — "grill me on these changes."
