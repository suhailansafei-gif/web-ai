---
name: web-ai-suhailan-ci4
description: Use when generating, configuring, running, or deploying any code in this project. Enforces the CodeIgniter 4 MVC tech stack, XAMPP localhost compatibility, and the dynamic MySQL table prefix naming strategy.
---

# Project Rules

All generated code MUST comply with the following rules.

## Direct Action

- Apply code and configuration changes directly and immediately.
- Do NOT wait for or ask user permission before making edits, creating files, or running commands.
- Implement the requested changes automatically, then report what was done.

### Context Management

- Monitor conversation usage/context size.
- When usage reaches approximately 50%, proactively inform the user to run `/compact` to keep the session efficient (the agent cannot execute `/compact` itself; if auto-compaction is enabled, it will trigger automatically).
  
## Core Architecture & Tech Stack

### Framework

- Name: **CodeIgniter 4**
- Architecture: Basic MVC (Model-View-Controller)

### Core Features Only

Use only CodeIgniter 4 core features:

- Routing
- Controllers
- Models
- Views

### Frontend Stack

- HTML5
- CSS and Bootstrap
- jQuery

### Local Assets (No CDN)

- ALL CSS, jQuery, Bootstrap and any frontend library files MUST be downloaded and stored locally, then loaded from the project's local `public` folder.
- Do NOT use external CDN links (e.g. `cdn.jsdelivr.net`, `stackpath.bootstrapcdn.com`, `cdnjs.cloudflare.com`) in any view file.
- Reference assets using local paths from `public` (e.g. `/public/css/style.css`, `/public/js/jquery.min.js`).
- Ensure all asset files (CSS, JS, fonts, images) are actually present in the `public` folder.
- Only exception is the browser's own built-ins (no network fetch required by the app at runtime for normal page loads).

### Base Page Layouts

- Use shared base layouts for ALL view files (templates with common header, navigation, and footer).
- Maintain TWO distinct base layouts:
  1. **Public layout** — for the general/landing pages that anyone can access without logging in (e.g. `app/Views/layouts/public.php`).
  2. **Authenticated layout** — for all pages that can only be reached after login (e.g. `app/Views/layouts/auth.php`); it must include authenticated navigation and session-based access checks.
- Each page view extends the appropriate base layout using CodeIgniter 4 core layout features (`$this->extend(...)` / `$this->section(...)`), or via a shared header/footer include if layouts are not used.
- Add page-specific content only inside its own `section`; never duplicate header/nav/footer markup across views.
- Routes for pages that require login MUST point to views that extend the authenticated layout and MUST be protected by a login/session filter.
- **REQUIRED**: Every view file that can only be reached after login MUST use `layouts/auth.php` (extend it via `$this->extend('layouts/auth')`). Do NOT use `layouts/public.php` for any authenticated page.
- 
### Strict Prohibitions

- **PROHIBITED** from using modern frontend frameworks (React, Vue, Angular).
- **PROHIBITED** from using Node.js or npm/build-tool-based environments.
- **PROHIBITED** from using complex architectures such as Microservices, Repository/Service Pattern.

## Localhost & XAMPP Compatibility

The system MUST run directly on a local XAMPP environment.

- **Runtime environment**: XAMPP (Apache + PHP + MySQL)
- **Access URL**: `http://localhost/{project-folder-name}`
- Use base CI4 `.env` settings appropriate for a local/development environment.
- Ensure the file structure and routing work without requiring special build commands.
  
## Dynamic Prefix MySQL Naming Strategy

Manages MySQL database design to avoid table conflicts.

- **Type**: MySQL
- **Prefix format**: `{project-folder-name}_`
- **Normalization**: Derive the prefix from the project folder name and replace any spaces or hyphens (`-`) with underscores (`_`), e.g. folder `web-ai` becomes prefix `web_ai_`, folder `my project` becomes `my_project_`. This keeps table names valid in MySQL without quoting.
- All tables MUST use a prefix generated from the project name to avoid table name collisions on localhost.
- Use basic CodeIgniter 4 Models (using the `$table` variable scheme with the relevant prefix).

## Google Authentication & Login

Rules for login integration with Google OAuth 2.0.

- If a user account/credentials table for login already exists, REUSE the same table — do not create a new one.
- Users MUST be able to log in using manual password input for any email account already registered.
- Users MUST also be able to choose Google Authentication login using the same email, provided that email is registered with Google.
- When generating the application, include the following Google OAuth 2.0 settings in the `.env` file:

```env
# Google OAuth 2.0 Configuration
# Get these from Google Cloud Console: https://console.cloud.google.com/apis/credentials
googleAuth.clientId = 'your_google_client_id'
googleAuth.clientSecret = 'your_google_secret_key'
googleAuth.redirectUri = '{URL}/auth/callback'
googleAuth.allowedDomain = ''
googleAuth.autoCreateAccount = true
```
