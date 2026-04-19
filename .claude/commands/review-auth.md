Review all authentication-related code for security vulnerabilities and best practices.

## Scope

Run this command after any auth-related change to catch regressions.

## Checklist

1. **Token Security**
   - JWT uses RS256, not HS256
   - Access tokens have 15min expiry
   - Refresh tokens stored in httpOnly secure cookies
   - No tokens logged or exposed in error responses

2. **Password Security**
   - bcrypt with cost factor 12
   - Never return password hash in any response
   - Password comparison uses bcrypt.compare, not string equality

3. **Input Validation**
   - All auth endpoints have request validation (joi/zod)
   - SQL uses parameterized queries, never string concatenation
   - Rate limiting on login, register, and refresh endpoints

4. **Error Handling**
   - No stack traces in production responses
   - Generic error messages for auth failures (don't reveal if email exists)
   - Failed login attempts logged but not detailed

Use subagents for parallel review of each section. Report findings as a security audit.
