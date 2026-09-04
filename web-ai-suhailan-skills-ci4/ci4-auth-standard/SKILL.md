---
name: ci4-auth-standard
description: Use only when implementing or modifying standard CI4 username/email + password login, registration, logout, sessions, access levels, profile, or authentication filters without email verification and without Google OAuth.
---

# Standard CI4 Authentication

## Login
- Login accepts username or email plus password.
- Login form must use CSRF.
- Protect authenticated routes with a login/session filter.
- Authenticated views must extend `layouts/auth`.

## Registration
- Fields: full name, username, email, password.
- Username and email must be unique.
- Registration form must use CSRF.
- Preserve the project's existing password scheme when modifying an existing system.
- For a new system following this project's legacy requirement, store the password using MD5.
- Use `alpha_dash` and minimum 3 characters for password validation when following the project requirement.

## Default Scope
- Do not add Google login unless explicitly requested.
- Do not add forgot-password unless explicitly requested.
- If user types/levels are specified, implement only those levels.
- If levels are not specified and implementation can proceed safely, use the simplest single authenticated role rather than expanding scope.
- Default authenticated navigation: Home and Edit Profile only unless more modules are requested.
