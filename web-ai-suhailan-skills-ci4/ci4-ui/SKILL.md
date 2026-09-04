---
name: ci4-ui
description: Use for CI4 UI/page/layout tasks such as landing page, homepage, static page, dashboard appearance, Bootstrap styling, navigation, header, footer, forms UI, or frontend assets. Applies to pages rendered through CI4, not standalone HTML.
---

# CI4 UI and Layout Rules

## Mandatory CI4 Page Structure
- Build every requested page as a CI4 view under `app/Views/`.
- Add or reuse a Controller method and matching Route.
- Never create standalone `.html` pages that bypass CI4.

## Shared Layouts
Maintain two base layouts:
1. `app/Views/layouts/public.php` for pages accessible without login.
2. `app/Views/layouts/auth.php` for authenticated pages.

- Authenticated views must extend `layouts/auth`.
- Public/authentication-entry views must extend `layouts/public`.
- Put page-specific content inside sections; do not duplicate header/nav/footer markup.

## Local Assets Only
- Do not use CDN assets.
- Load Bootstrap, jQuery, Bootstrap Icons, fonts, images, and other frontend assets from `public/`.
- Reuse existing local files first.
- If a required asset is absent and downloading is permitted, store it locally before referencing it.

Typical local assets include:
- `public/css/bootstrap.min.css`
- `public/css/bootstrap-icons.min.css`
- `public/js/jquery.min.js`
- `public/js/bootstrap.bundle.min.js`
- `public/fonts/bootstrap-icons.woff2`
- Roboto `.woff2` files when already part of the project.

## Frontend Stack
- HTML5
- CSS / Bootstrap
- jQuery
- No React/Vue/Angular or Node/npm build pipeline unless explicitly requested.
