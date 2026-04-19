---
name: auth-review
description: when implementing or modifying authentication code, review for security vulnerabilities before committing
context: fork
---

Review authentication-related code for security issues and best practice violations.

## Review Focus

- **Token exposure risks**: check logs, responses, error messages
- **SQL injection**: verify parameterized queries in all user-facing queries
- **Rate limiting**: ensure auth endpoints have rate limiters
- **Password handling**: bcrypt.compare (not string match), no hash in responses
- **JWT algorithm**: enforce RS256, reject none/HS256

## Gotchas

- Claude tends to default to HS256 for JWT — enforce RS256
- Claude may forget to hash passwords in seed/migration data
- bcrypt.compare vs bcrypt.hash: sometimes confused in login flows
- Express middleware order matters: rate-limit before auth, auth before validation
- Refresh token rotation: Claude often forgets to invalidate old refresh tokens

## References

- references/owasp-auth-cheatsheet.md
