# User Registration Spec

## Endpoint
`POST /api/auth/register`

## Request Body
```json
{
  "email": "user@example.com",
  "password": "SecureP@ss123",
  "username": "johndoe"
}
```

## Validation Rules
- **email**: valid email format, max 254 chars, unique in DB
- **password**: min 8 chars, at least 1 uppercase, 1 lowercase, 1 digit, 1 special char
- **username**: 3-30 chars, alphanumeric + underscores only, unique in DB

## Success Response (201)
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
- **400**: Validation error (invalid email, weak password, etc.)
- **409**: Email or username already exists
- **429**: Rate limit exceeded (max 3 registrations per IP per hour)

## Business Rules
- Password hashed with bcrypt (cost 12) before storage
- Email stored lowercase
- On success: create user, issue access + refresh token pair
- Refresh token stored in httpOnly secure cookie AND in DB for revocation
- Welcome email queued (non-blocking, don't fail registration if email fails)

## Security
- Rate limited: 3 requests per IP per hour
- Input sanitized before validation
- No password in any log or response
