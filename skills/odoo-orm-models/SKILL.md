---
name: odoo-orm-models
description: Design, extend, debug, or review Odoo ORM models, fields, computed fields, constraints, methods, and business logic.
---

# Odoo ORM and model work

1. Detect the Odoo version from repository configuration, running server/source, manifest conventions, or explicit user input. Verify APIs against that version.
2. Read the model and its callers, field dependencies, inherited definitions, and tests before editing.
3. Follow recordset semantics and preserve context, access rights, company boundaries, and transaction behavior.

## Review/design checklist

- Model identity: `_name`, `_inherit`, `_description`, `_rec_name`, ordering, and abstract/transient/persistent behavior fit the requirement.
- Fields: correct type, relation, `ondelete`, `copy`, `index`, `required`, `readonly`, `tracking`, and company behavior; avoid stored computed fields without a reason.
- Computed fields: complete `@api.depends` declarations (including relational paths as supported by this version), correct inverse/search where needed, and no hidden writes in compute methods.
- Related fields and defaults: avoid expensive or context-dependent defaults; distinguish unset from false/empty where relevant.
- Constraints: use supported ORM decorators/APIs for the detected release; handle multi-record calls and clear validation messages.
- Methods: return contracts and side effects are explicit; batch operations where appropriate; avoid N+1 queries and direct SQL unless demonstrably necessary.
- Security: access rights are not implied by view visibility; enforce server-side authorization and avoid unsafe `sudo()`.
- Compatibility: check overrides, `super()` chain, method signatures, and framework callers in the exact version.
- Tests: cover normal, boundary, multi-record, access, company, and regression cases as appropriate.

Do not present a remembered decorator/API as version-independent. Search the local source and versioned official documentation when behavior is uncertain.
