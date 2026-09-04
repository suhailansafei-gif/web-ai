---
name: ci4-datatables
description: Use only when a CI4 page displays or modifies tabular data, DataTables, pagination, table searching/sorting, or Excel/PDF table export.
---

# CI4 DataTables Rules

- Use DataTables by default for data tables.
- Enable pagination by default.
- Enable Excel export using DataTables Buttons `excelHtml5`.
- Enable PDF export using DataTables Buttons `pdfHtml5`.
- Keep all DataTables dependencies local in `public/`; never use CDN.
- Initialize tables in a DOM-ready jQuery handler.

Expected local assets may include:
- `public/css/dataTables.bootstrap5.min.css`
- `public/css/buttons.bootstrap5.min.css`
- `public/js/jquery.dataTables.min.js`
- `public/js/dataTables.bootstrap5.min.js`
- `public/js/dataTables.buttons.min.js`
- `public/js/buttons.bootstrap5.min.js`
- `public/js/buttons.html5.min.js`
- `public/js/jszip.min.js`
- `public/js/pdfmake.min.js`
- `public/js/vfs_fonts.js`

Reuse existing copies first. If required files are missing and download is allowed, store them locally.
