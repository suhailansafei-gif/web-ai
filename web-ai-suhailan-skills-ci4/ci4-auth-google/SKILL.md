---
name: ci4-auth-google
description: Use only when implementing, configuring, or debugging Google OAuth 2.0 sign-in/login for the CI4 project.
---

# Google OAuth 2.0 for CI4

- Reuse the existing user/account table if one exists.
- Do not create a second credentials table unnecessarily.
- Manual password login may coexist with Google sign-in for the same registered email.
- Only add Google authentication when explicitly requested.

Add Google OAuth settings to `.env`:
```env
googleAuth.clientId = 'your_google_client_id'
googleAuth.clientSecret = 'your_google_secret_key'
googleAuth.redirectUri = '{URL}/auth/callback'
googleAuth.allowedDomain = ''
googleAuth.autoCreateAccount = true
```

- Keep secrets in `.env`, not in controllers or views.
- Implement the callback through CI4 routing/controller logic.
