---
name: odoo-verification
 description: Verify Odoo code changes, fixes, and migrations before claiming completion; report concrete evidence and remaining gaps.
---

# Odoo verification before completion

Use before reporting a feature, fix, installation, or migration as complete. Verification must match the claim and available environment.

## Evidence checklist

- Re-read the diff and confirm only intended files/behavior changed; inspect for debug statements, secrets, generated files, unrelated edits, and unsafe data operations.
- Run formatting/lint/type/static checks that the repository actually configures and that apply to the changed files.
- Run focused Odoo tests for the changed behavior and relevant access/company boundaries. If meaningful, run module install/update and view validation in a disposable database.
- For migrations, test on a representative database copy using the supported path and verify record counts, relations, business invariants, user access, and critical workflows.
- Inspect command exit codes and relevant logs. Do not rely solely on “server starts” or tests that did not exercise the changed behavior.
- If checks cannot run (missing Odoo source/runtime, PostgreSQL, Enterprise addons, test database, dependencies, or credentials), state the exact blocker and which checks remain unverified. Never imply success from static inspection alone.

## Report

Give exact commands/checks and concise results, distinguish passed/failed/skipped, and list residual risks. Use statements proportional to evidence: “static checks passed” is not “the module was successfully installed,” and “test database upgrade passed” is not “production migration is safe.”
