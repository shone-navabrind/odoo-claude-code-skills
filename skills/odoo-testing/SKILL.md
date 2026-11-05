---
name: odoo-testing
description: Write, select, or run Odoo tests and diagnose module installation, upgrade, or regression failures.
---

# Odoo testing

Determine the Odoo version, test framework conventions, database configuration, and available executables first. Use the narrowest meaningful test scope.

## Test design

- Test observable business behavior, not just implementation details.
- Cover success, validation, access denied, multi-record behavior, company boundaries, and regressions where relevant.
- Reuse project fixtures and standard Odoo test utilities for the detected version.
- Ensure test files are imported and test tags match the intended run.
- Keep tests isolated and deterministic; avoid external network dependencies and real production data.
- Add upgrade/migration tests for data transformations where feasible, including repeatability and preservation of unaffected data.

## Running checks

- Read this project's README, CI, and scripts to find its canonical test invocation; do not assume a universal command/database name.
- Prefer targeted module tests and relevant install/update checks. Quote the exact command and outcome.
- If Odoo, PostgreSQL, a test database, or required Enterprise addons are unavailable, state that explicitly and do not imply runtime verification.
- Separate test failures introduced by the change from environment/setup failures using logs and a baseline where practical.

Report what passed, failed, was skipped, and remains unverified.
