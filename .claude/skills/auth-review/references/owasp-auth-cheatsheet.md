# OWASP Authentication Cheatsheet — Key Points

## Password Storage
- Use bcrypt, scrypt, or Argon2id
- bcrypt cost factor >= 10 (we use 12)
- Never store plaintext passwords

## JWT Best Practices
- Use asymmetric algorithms (RS256/ES256)
- Never use `none` algorithm
- Short-lived access tokens (15 min)
- Longer refresh tokens with rotation
- Store refresh tokens server-side for revocation capability

## Session Management
- Regenerate session ID after login
- Invalidate all sessions on password change
- Implement concurrent session limits

## Login Protection
- Rate limit login attempts (e.g., 5 per minute per IP)
- Implement account lockout after N failed attempts
- Use generic error messages ("Invalid credentials")
- Log failed attempts with IP and timestamp

## Password Reset
- One-time use tokens with short expiry (1 hour)
- Send reset link, not new password
- Invalidate all existing sessions after password reset
- Notify user of password change via email
