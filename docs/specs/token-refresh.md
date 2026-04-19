# Token Refresh Spec

## Endpoint
`POST /api/auth/refresh`

## Request
Refresh token sent via httpOnly secure cookie (`refreshToken`)

## Success Response (200)
```json
{
  "tokens": {
    "accessToken": "jwt...",
    "refreshToken": "jwt..."
  }
}
```

## Error Responses
- **401**: Invalid or expired refresh token
- **401**: Refresh token revoked (user logged out)

## Business Rules
- Validate refresh token signature and expiry
- Check token exists in DB (not revoked)
- On success: rotate refresh token (invalidate old, issue new)
- Update cookie with new refresh token
- If refresh token is invalid/reused: revoke ALL refresh tokens for that user (refresh token rotation attack detection)

## Security
- Single-use refresh tokens (rotation)
- Reuse detection triggers full revocation
- Access token in response body, refresh token in cookie only
