---
name: ci4-core
description: Core CodeIgniter 4 project rules. Use when creating or modifying CI4 controllers, models, views, routes, configuration, or project structure. Do not use for auth-specific, DataTables-specific, database-schema-specific, or XAMPP deployment tasks unless those topics are directly requested.
---

# CI4 Core Rules

## Direct Action
- Apply requested code/configuration changes directly.
- Do not ask for permission before editing files or running required commands.
- Report completed changes afterward.

## Architecture
- Framework: CodeIgniter 4.
- Use basic MVC only: Routes, Controllers, Models, Views.
- Avoid React, Vue, Angular, Node.js, npm, microservices, Repository Pattern, and Service Pattern unless explicitly requested.
- Frontend baseline: HTML5, CSS/Bootstrap, jQuery.

## CI4 Pages
- All pages must be implemented inside CI4, never as standalone HTML.
- Create page views under `app/Views/`.
- Serve views using a Controller method and matching route in `app/Config/Routes.php`.
- Use CI4 layout/section features rather than duplicating shared markup.

## Form Handling
- Compare `getMethod()` results in uppercase.
- Do not enable CSRF for every form by default.
- Login and registration forms must use CSRF.
- Do not create a contact form unless explicitly requested.

## Existing Project First
- Preserve the existing project structure and conventions where practical.
- Reuse existing controllers, models, views, routes, tables, and assets when they already satisfy the requested feature.
