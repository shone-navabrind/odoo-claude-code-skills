---
description: Review an addon for Odoo compatibility, security, data risks, tests, and third-party provenance without editing by default.
argument-hint: [addon path or review focus]
---

Use `odoo-review` and, for migrations, `odoo-addon-inventory`. Inspect repository instructions, actual diff, version/edition, module manifest/dependencies, relevant callers, views/security, and tests. Classify origin only from evidence. For third-party modules, ask whether online compatibility lookup is allowed; then present verified upstream release vs local port as a simple choice if relevant. Give actionable findings with paths/lines and severity, separate confirmed defects from uncertainty, and do not edit unless asked.
