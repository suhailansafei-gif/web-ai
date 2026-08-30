---
name: web-ai-suhailan-ci4
description: Use when the user asks to generate, build, modify, configure, run, debug, or deploy ANY code in this project - a CodeIgniter 4 (CI4) MVC web app on XAMPP localhost with MySQL. Triggers on requests involving; controllers, models, views, routes, layouts (public/auth), forms, login/register/forgot-password, Google OAuth login, DataTables with Excel/PDF export, database tables/schema, .env settings, or any .php work here. TRIGGERS ALWAYS on "web static", "static page(s)", "landing page", "homepage", "static HTML page", "web page", "page(s)", or any UI/layout request, even when NOT explicitly CI4 - ALL of it MUST be built inside the CI4 structure as a view served through a Controller/Route (never standalone HTML). Enforces CI4 core MVC, local assets (no CDN, DataTables from public), XAMPP localhost (`localhost/<project-folder>`), and dynamic MySQL table prefix naming (`{folder}_`).
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
- Capture and report the time spent for each responses completion.
  
## Core Architecture & Tech Stack

### Framework

- Name: **CodeIgniter 4**
- Architecture: Basic MVC (Model-View-Controller)
- Download fresh CodeIgniter 4 from https://github.com/codeigniter4/framework/archive/refs/tags/v4.7.4.zip if available.

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

### Form Handling
- Set to uppercase comparison for all conditions that retrieve the CI4 getMethod() function.
- Do not apply CSRF protection for all forms EXCEPT for explicitly required by the user. However for login related forms such as login form and register new user form should always protected with CSRF.

### Local Assets (No CDN)
- ALL CSS, jQuery, Bootstrap and any frontend library files MUST be downloaded and stored locally, then loaded from the project's local `public` folder.
- Download all required bootstrap icons.
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

### Table Display

- For any table display, use a table library (e.g. **DataTables**) BY DEFAULT.
- Enable the following features by default:
  - **Pagination** (paging)
  - **Export to Excel** (e.g. DataTables Buttons `excelHtml5`)
  - **Export to PDF** (e.g. DataTables Buttons `pdfHtml5`)
- The table library and ALL its assets (DataTables core, Buttons, JSZip, pdfmake, and related CSS/JS) MUST be downloaded and stored in the project's local `public` folder — everything stays local.
- Do NOT load the table library or export plugins from any CDN.
- Reference the table assets using local paths from `public` (e.g. `/public/plugins/jquery.dataTables.min.js`, `/public/plugins/dataTables.bootstrap5.min.js`).
- Initialize the table in a DOM-ready (`$(document).ready`) script and wire the export buttons (Excel/PDF) into the toolbar.

### Strict Prohibitions

- **PROHIBITED** from using modern frontend frameworks (React, Vue, Angular).
- **PROHIBITED** from using Node.js or npm/build-tool-based environments.
- **PROHIBITED** from using complex architectures such as Microservices, Repository/Service Pattern.

## Mandatory CI4 Structure for ALL Pages (Including Static)

- **ALL** web pages, "web static", landing pages, homepages, and any UI/page request MUST be built **inside the CodeIgniter 4 MVC structure**, even if the user only asks for a simple/static page. This rule applies to every request.
- Every page MUST be implemented as a CI4 **view** under `app/Views/` (in the appropriate folder), plus a **Controller** method and a matching **Route** in `app/Config/Routes.php` to serve it.
- Every view MUST extend the correct base layout (`layouts/public` for open pages, `layouts/auth` for pages behind login) using `$this->extend(...)` / `$this->section(...)`.
- **PROHIBITED** from outputting standalone `.html` files, inline-only HTML, or raw static markup that bypasses the CI4 structure. Never create a page that is not routed and rendered through a CI4 controller/view.
- Assets are always served from the local `public` folder (see "Local Assets (No CDN)").

## Localhost & XAMPP Compatibility

The system MUST run directly on a local XAMPP environment.

- **Runtime environment**: XAMPP (Apache + PHP + MySQL)
- **Access URL**: `http://localhost/{project-folder-name}`
- Use base CI4 `.env` settings appropriate for a local/development environment.
- Ensure the file structure and routing work without requiring special build commands.
- Set .htaccess at the root folder to `public` folder
  
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

## Standard Login (Email & Password)

Rules for the non-Google login flow with no email validation.

- If the login form is NOT Google authentication, create a STANDARD login flow with these pages:
  - **Login** — email + password sign-in form. Use CSRF protection.
  - **Register** — sign-up form with full name, phone number, username and password; Store password in md5 hashed (never plaintext). Use CSRF protection.
  - **Forgot Password** — No need to add.
- **RESTRICTION**: Do NOT add Google authentication login by default when creating the standard (Email & Password) login flow. Only add Google login if the user explicitly requests it.
- Ask the "user types/levels" for the login if not specified. Create only page with "Home" and "Edit Profile" menu. Create simple landing page with unique color schema that differentiate the user type/level.


## Standard Login with Google Email Validation

If the "forgot password" and "new user registration" is required to be validated with email, use the following rules. Remove any existing "standard login (Email & Password)" controllers and views.

- If the login form is NOT Google authentication, create a STANDARD login flow with these pages:
  - **Login** — email + password sign-in form. Use CSRF protection.
  - **Register** — sign-up form with full name, email and phone number(optional); Validate that the email is unique. Sends a register account link/token. Once the link was clicked, asked for the password input. Store password in md5 hashed (never plaintext). Use CSRF protection.
  - **Forgot Password** — form that accepts the registered email and sends a password-reset link/token.
- **RESTRICTION**: Do NOT add Google authentication login by default when creating the standard (Email & Password) login flow. Only add Google login if the user explicitly requests it.
- Ask the "user types/levels" for the login if not specified. Create only page with "Home" and "Edit Profile" menu. Create simple landing page with unique color schema that differentiate the user type/level.
- Send registration verification and password-reset emails using the CodeIgniter 4 core `Email` library.
- Deliver mail through **Gmail SMTP** using the account owner's **Google App Password** (see notes in the `.env` block below).
- Create the view files at `app/Views/auth/login.php`, `app/Views/auth/register.php`, and `app/Views/auth/forgot_password.php` (these are reachable without login, so they use the public layout).
- Include the following email settings in the `.env` file:

```env
# Email (Gmail SMTP)
email.protocol       = smtp
email.smtpHost       = smtp.gmail.com
email.smtpPort       = 587
email.smtpUser       = 'your.email@gmail.com'
# Get your 16-digit Google App Password here: https://myaccount.google.com/apppasswords
# (enable 2-Step Verification on the Google account first).
# The App Password is generated in 4 blocks of 4 characters, e.g. 'abcd efgh ijkl mnop'.
# The spaces/dashes may be removed OR kept - Gmail only checks the 16 characters, both forms work.
email.smtpPass       = 'your_16_digit_app_password'
email.smtpCrypto     = tls
# email.fromEmail MUST be the SAME address as email.smtpUser above (Gmail enforces this for SMTP auth).
email.fromEmail      = 'your.email@gmail.com'
email.fromName       = '{Project-Name}'
```
