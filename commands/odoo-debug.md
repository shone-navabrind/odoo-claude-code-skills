---
description: Diagnose an Odoo exception or unexpected behavior from the provided error and repository evidence.
argument-hint: [error message, traceback, or symptom]
---

Use `odoo-systematic-debugging` and `odoo-verification`, plus relevant module/ORM/security skills. Analyze $ARGUMENTS. Establish the exact Odoo version and environment, identify the earliest meaningful project-owned traceback frame, trace callers and configuration, and test plausible causes before editing. Avoid speculative or repeated patches; change one root cause at a time and add a regression test when feasible. Do not run repair or install/update actions on production. Report root-cause evidence, fix, exact checks run, and unresolved uncertainty.
