# Password Reset Spec

## Endpoint 1: Request Reset
`POST /api/auth/forgot-password`

### Request Body
```json
{
  "email": "user@example.com"
}
```

### Success Response (200)
```json
{
  "message": "If an account with that email exists, a reset link has been sent"
}
```

### Business Rules
- Always return same response whether email exists or not (prevent enumeration)
- Generate one-time reset token (crypto.randomBytes, 1-hour expiry)
- Store token hash (not plaintext) in DB
- Send reset link via email (non-blocking)
- Rate limited: 3 requests per IP per hour

## Endpoint 2: Confirm Reset
`POST /api/auth/reset-password`

### Request Body
```json
{
  "token": "reset-token-from-email",
  "newPassword": "NewSecureP@ss456"
}
```

### Success Response (200)
```json
{
  "message": "Password reset successfully"
}
```

### Business Rules
- Validate token: not expired, not used, hash matches
- Invalidate ALL refresh tokens for this user (force re-login on all devices)
- Hash new password with bcrypt cost 12
- Mark reset token as used
- Send password change notification email

## Security
- Reset tokens are one-time use
- Token stored as hash, never plaintext in DB
- Force re-login on all devices after reset
- Rate limit both endpoints
