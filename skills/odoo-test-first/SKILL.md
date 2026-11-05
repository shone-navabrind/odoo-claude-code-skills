---
name: odoo-test-first
description: Implement Odoo behavior changes with focused tests first when a meaningful, runnable regression test can be written.
---

# Odoo test-first implementation

Prefer a test-first loop for new behavior and bug fixes when the repository has a usable Odoo test environment. Adapt rather than ritualize it: do not write fake tests, modify unrelated tests to force a pass, or claim a red/green cycle when the environment cannot run it.

## Red → green → refactor

1. Understand existing behavior, Odoo version, fixtures, and test conventions. Identify the smallest user-observable behavior to cover.
2. Add a focused test that fails for the intended reason. Run it and inspect the failure. If it fails during setup or for an unrelated reason, fix the test setup before implementation.
3. Implement the smallest change that satisfies the behavior while respecting ORM/security/data contracts.
4. Re-run the focused test and relevant neighboring tests. Refactor only while keeping tests green.
5. Inspect the diff and run relevant install/update/static checks; report exact commands and limitations.

## When test-first is unavailable

If there is no runtime/database, required edition, or viable fixture, describe the blocker. Use a static analysis or isolated reproducible check where it provides evidence, and add a test for execution in CI if possible. Do not guess test commands; inspect project CI and `odoo-bin --help` for the target version.

For data migrations, use representative fixtures or a disposable DB copy and test preservation/idempotence. Never use a production database as the red/green environment.
