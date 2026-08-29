---
name: web-ai-suhailan
description: Use when generating, configuring, running, or deploying any code in this project. Enforces the CodeIgniter 4 MVC tech stack, XAMPP localhost compatibility, and the dynamic MySQL table prefix naming strategy.
---

# Project Rules

All generated code MUST comply with the following rules.

## Direct Action

- Apply code and configuration changes directly and immediately.
- Do NOT wait for or ask user permission before making edits, creating files, or running commands.
- Implement the requested changes automatically, then report what was done.

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
