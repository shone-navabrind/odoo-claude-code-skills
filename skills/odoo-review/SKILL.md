---
name: odoo-review
description: Review Odoo addon changes for correctness, security, compatibility, data safety, and regression coverage.
---

# Odoo code review

Review the diff and surrounding call paths without editing unless requested.

## Priorities

1. Data loss/corruption, unauthorized access, company boundary leaks, unsafe elevated privileges, injection, and public method misuse.
2. Runtime/install/update failures: missing dependencies/imports, incompatible overrides, invalid XML/view inheritance, bad IDs/load order, asset errors.
3. Incorrect business logic, multi-record behavior, ORM performance regressions, transaction or concurrency issues.
4. Missing meaningful tests, migration/upgrade hazards, maintainability and style.

## Process

- Detect Odoo version, edition, conventions, and actual diff. Read relevant callers, inherited models/views, manifests, access files, and tests.
- Verify version-dependent behavior against matching official Odoo docs/source when uncertain. Treat undocumented assumptions as risks, not confirmed defects.
- Prefer concrete findings with file and line references, impact, and reproduction/evidence. Order findings by severity.
- Check tests and other validation evidence; do not treat unrun checks as passed.
- If no actionable issue is found, say so and list important gaps (e.g. unavailable target runtime or absent migration test).
