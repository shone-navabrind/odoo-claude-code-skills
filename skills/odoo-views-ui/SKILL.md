---
name: odoo-views-ui
description: Create or modify Odoo XML views, actions, menus, wizards, reports, and UI behavior.
---

# Odoo views and UI

Inspect the target version and nearby module patterns first. Odoo view syntax and frontend behavior evolve; validate against the exact release instead of copying XML from another version.

## Checklist

- Identify the intended view type, action, menu parent, model, and access group.
- For inherited views, use the correct external ID and a stable, minimally invasive XPath. Confirm the target node exists in the target version.
- Follow the target version's view architecture and expression syntax. Do not assume legacy modifiers, widgets, or attributes are still valid.
- Keep business validation and authorization in server-side model logic; UI visibility is not security.
- Use context/domain deliberately; avoid unsafe evaluation of user-controlled values.
- Ensure XML IDs are unique, dependencies are declared, and files load in the correct manifest order.
- For QWeb/reports, preserve escaping, translations, company context, and paper/report behavior.
- For JS/SCSS assets, inspect the target release's asset bundles and neighboring addon patterns; avoid guessing bundle names.
- Test installation/update and relevant flows; check logs for view validation errors.

When migrating a view, compare the source and target core view definitions and official versioned guidance. Change only the affected architecture and provide the evidence.
