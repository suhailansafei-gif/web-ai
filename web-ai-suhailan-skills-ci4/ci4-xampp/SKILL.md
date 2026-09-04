---
name: ci4-xampp
description: Use only for local XAMPP setup, localhost URL/routing problems, Apache .htaccess, CI4 .env development settings, installing CI4 into an empty project folder, or making the project run under localhost/<project-folder>.
---

# CI4 XAMPP / Localhost Rules

- Runtime: XAMPP with Apache, PHP, and MySQL.
- Target URL: `http://localhost/{project-folder-name}`.
- Use CI4 `.env` settings appropriate for local/development use.
- Ensure routing works without Node/npm/build commands.
- Configure root `.htaccess` so requests are served through the `public` folder when required by the project's XAMPP setup.

## Fresh CI4 Project
- If the current project folder does not contain CodeIgniter 4 and the user asks to initialize/build the CI4 project, install a compatible CI4 release.
- Do not download/reinstall CI4 merely for ordinary modifications to an existing project.
