---
name: ci4-database
description: Use for MySQL schema, tables, fields, relationships, migrations/SQL, CI4 Models, or database naming in this project. Do not load for UI-only changes.
---

# CI4 Database Rules

## Database
- DBMS: MySQL.
- Use basic CodeIgniter 4 Models.

## Dynamic Table Prefix
- Derive the table prefix from the project folder name.
- Format: `{project_folder}_`.
- Normalize spaces and hyphens to underscores.
- Examples:
  - `web-ai` -> `web_ai_`
  - `my project` -> `my_project_`
- Apply the prefix to all newly created project tables.
- Configure each CI4 Model `$table` value with the relevant prefixed table name.

## Reuse Existing Tables
- Before creating a new table, inspect whether an appropriate existing table can be reused.
- In particular, reuse an existing user/account table for authentication instead of duplicating it.
