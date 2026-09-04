---
name: ci4-auth-email
description: Use only when CI4 registration requires real email verification, password-reset email, forgot-password flow, verification tokens, Gmail SMTP, or Google App Password configuration.
---

# CI4 Authentication with Email Validation

## Public Auth Views
Use:
- `app/Views/auth/login.php`
- `app/Views/auth/register.php`
- `app/Views/auth/forgot_password.php`

These pages use the public layout.

## Registration Verification
- Registration collects full name, username, email, and begins email verification.
- Username and email must be unique.
- Send a registration verification link/token.
- After verification, request/set the password according to the project flow.
- Login and registration-related forms use CSRF.

## Forgot Password
- Accept the registered email.
- Send a password-reset link/token.

## Email Delivery
- Use CodeIgniter 4 core `Email` library.
- Send through Gmail SMTP with a Google App Password.

Example `.env` keys:
```env
email.protocol = smtp
email.smtpHost = smtp.gmail.com
email.smtpPort = 587
email.smtpUser = 'your.email@gmail.com'
email.smtpPass = 'your_16_digit_app_password'
email.smtpCrypto = tls
email.fromEmail = 'your.email@gmail.com'
email.fromName = '{Project-Name}'
```

- `email.fromEmail` should match `email.smtpUser` for Gmail SMTP.
- Do not add Google OAuth sign-in unless explicitly requested.
