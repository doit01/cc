# CLAUDE.md

## Project: Blog Auth API
Stack: Node.js + Express + PostgreSQL + TypeScript

## Commands
- Build: `npm run build`
- Test: `npm test`
- Dev: `npm run dev`
- Lint: `npm run lint`
- Migrate: `npm run db:migrate`

## Architecture
```
src/
├── routes/        — route handlers (thin, delegate to services)
├── services/      — business logic (auth, token management)
├── repositories/  — database queries (raw SQL via pg)
├── middleware/     — auth, validation, error handling, rate limiting
└── models/        — TypeScript interfaces & type guards
```

## Code Style
- Strict TypeScript: no `any`, use `unknown` + type guard
- Async/await everywhere, no raw promises
- Error handling: throw AppError subclasses, caught by central middleware
- Logging: use winston, never console.log

<important if="implementing authentication">
## Auth Rules
- Use bcrypt for password hashing (cost factor 12)
- JWT with RS256, never HS256
- Access token: 15min, Refresh token: 7d
- Never log or expose tokens in responses beyond the auth endpoints
- All auth routes must have rate limiting (express-rate-limit)
- Refresh tokens stored in httpOnly secure cookies, not localStorage
</important>

<important if="writing tests">
## Test Rules
- Jest with ts-jest
- DB tests need `--runInBand` flag
- Factory functions for test data, no hardcoded fixtures
- Mock at boundaries only (external APIs, not internal modules)
</important>

## Gotchas
- PostgreSQL uses `RETURNING *` after INSERT
- bcrypt.hash is async — never use sync version in hot paths
- JWT verify throws — always wrap in try/catch
- Don't use `any` type — use `unknown` + type guard
- Express error handlers must have 4 parameters or they won't catch
