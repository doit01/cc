# User Login Spec

## Endpoint
`POST /api/auth/login`

## Request Body
```json
{
  "email": "user@example.com",
  "password": "SecureP@ss123"
}
```

## Success Response (200)
```json
{
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "username": "johndoe"
  },
  "tokens": {
    "accessToken": "jwt...",
    "refreshToken": "jwt..."
  }
}
```

## Error Responses
- **401**: Invalid credentials (generic message, don't reveal if email exists)
- **429**: Rate limit exceeded (max 5 attempts per IP per 15 minutes)

## Business Rules
- Compare password with bcrypt.compare (never string equality)
- On success: rotate refresh token (invalidate old, issue new)
- Failed login: log IP + timestamp (NOT the attempted password)
- After 5 failed attempts from same IP: 15-minute lockout

## Security
- Generic error messages for all auth failures
- Rate limited: 5 requests per IP per 15 minutes
- Refresh token in httpOnly secure cookie
