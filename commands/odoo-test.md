---
description: Find and run the narrowest relevant tests or checks for an Odoo addon, then explain results.
argument-hint: [module path or behavior]
---

Use `odoo-test-first` and `odoo-verification`. Inspect project CI, test configuration, addon path, and available Odoo/PostgreSQL runtime. Identify a targeted check for $ARGUMENTS, run it if possible, and report exact commands and results. Do not run destructive operations against a production database. Clearly label checks that are unavailable or skipped.
