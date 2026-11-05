---
name: odoo-module-development
description: Build or modify Odoo addons and custom modules. Use when creating a module, implementing a feature, extending core behavior, or exploring an existing addon.
---

# Odoo module development

Work from evidence in the checked-out project; do not assume a generic Odoo layout or version.

## Efficient workflow

1. Identify the repository root, addon paths, target Odoo version/branch, edition, and existing conventions. Inspect nearby modules, `__manifest__.py`, tests, and relevant configuration before proposing a structure.
2. Restate the requested behavior as a small acceptance checklist. Ask only for essential missing business rules; otherwise make conservative assumptions explicit.
3. Trace the relevant model/view/security/test paths with targeted searches. Read direct dependencies and inherited views before editing. Avoid broad repository exploration when a narrow search answers the question.
4. Implement the smallest cohesive change. Reuse project conventions and supported APIs for the detected Odoo version. Do not invent models, fields, XML IDs, or external dependencies.
5. Add or update tests for behavior, access boundaries, and regressions. Consider multi-company and multi-record behavior where relevant.
6. Run targeted lint/static checks and the narrowest applicable Odoo tests if the environment supports them. Do not claim tests passed unless they were run. Report blocked checks.
7. Summarize changed files, behavior, checks, assumptions, and any upgrade/deployment steps.

## Module anatomy checklist

Use only pieces needed for the feature; a minimal module need not contain every directory.

- `__manifest__.py`: accurate name/version/dependencies/data/assets/installability; version format follows repository conventions.
- `models/`: imports in `__init__.py`; ORM fields and methods; avoid side effects at import time.
- `views/`: XML records with stable IDs and correct inheritance; include in manifest data.
- `security/`: groups, ACLs, record rules, least privilege; load in dependency order.
- `data/`: only intentional, safely repeatable records; distinguish demo data.
- `static/`: assets registered using the target version's conventions.
- `tests/`: imported test modules and correct test tags/fixtures for the checked-out version.
- `migrations/`: only when a real versioned upgrade requires a data/schema transformation.

## Odoo-specific cautions

- `self` is a recordset: methods must generally handle multiple records. Use `ensure_one()` only when the contract truly requires one record.
- Preserve ORM semantics, access checks, company context, translations, and transaction behavior. Do not bypass the ORM with SQL unless justified and safe.
- Do not use `sudo()` to hide access errors. Explain and limit any elevation; validate user-controlled inputs and company boundaries.
- Use ORM APIs and decorators supported by the actual version. Confirm behavior in installed source/docs rather than relying on memory.
- Keep dependencies explicit, avoid circular imports, and don't modify Odoo core when a supported addon extension suffices.
- Use `_inherit` to extend existing models; use `_name` only when defining a new model or intentionally using documented delegation/inheritance patterns.
- Do not change generated/vendor files or unrelated module behavior.

## Response format

Give a short implementation summary, key design/security decisions, exact checks run (or why unavailable), and unresolved assumptions. For migration-relevant changes, name the affected Odoo versions.
