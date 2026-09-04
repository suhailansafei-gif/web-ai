# Split OpenCode Skills for CI4 Project

The original monolithic skill was split so OpenCode can select only the rules relevant to the current task.

## Skills

| Skill | Loads when |
|---|---|
| `ci4-core` | Controllers, models, views, routes, core CI4 structure |
| `ci4-ui` | Landing page, homepage, UI, Bootstrap, layouts, frontend assets |
| `ci4-datatables` | Tables, DataTables, pagination, Excel/PDF export |
| `ci4-database` | MySQL schema, tables, Models, table prefix |
| `ci4-auth-standard` | Normal login/register/session/profile |
| `ci4-auth-email` | Email verification, forgot password, Gmail SMTP |
| `ci4-auth-google` | Google OAuth login |
| `ci4-xampp` | XAMPP, localhost, `.htaccess`, local install/configuration |

## Why this reduces unnecessary loading

The original skill description triggered on almost everything (`ANY code`, `page(s)`, `static HTML`, auth, database, DataTables, deployment). That makes unrelated instructions candidates for loading together.

Each new skill now has a narrow `description`. Avoid phrases such as `ALWAYS`, `ANY code`, or broad catch-all triggers in specialized skills.

## Suggested behavior

A UI request may load:
- `ci4-core`
- `ci4-ui`

A table page may load:
- `ci4-core`
- `ci4-ui`
- `ci4-datatables`
- optionally `ci4-database` if schema/query changes are involved

A standard login request may load:
- `ci4-core`
- `ci4-ui`
- `ci4-auth-standard`
- optionally `ci4-database`

Email reset should add only `ci4-auth-email`; Google login should add only `ci4-auth-google`.

## Important design rule

Do not create one new master skill whose description again says it applies to every prompt. That would recreate the same token-loading problem. Keep `ci4-core` small and let specialized skills be selected by their descriptions.
