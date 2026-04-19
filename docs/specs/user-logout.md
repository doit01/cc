# User Logout Spec

## Endpoint
`POST /api/auth/logout`

## Request
Requires valid access token in Authorization header.

## Success Response (200)
```json
{
  "message": "Logged out successfully"
}
```

## Business Rules
- Revoke the refresh token from DB
- Clear the refreshToken cookie
- Access token naturally expires (15 min) — no server-side blacklist needed for MVP
- If no valid session found, still return 200 (idempotent)

## Security
- Must require authentication (valid access token)
- Clear cookie with same options as when set (httpOnly, secure, sameSite)
