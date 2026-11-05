---
description: Find and run the narrowest relevant tests or checks for an Odoo addon, then explain results.
argument-hint: [module path or behavior]
---

Use the `odoo-testing` skill. Inspect project CI, test configuration, addon path, and available Odoo/PostgreSQL runtime. Identify a targeted test/check for $ARGUMENTS, run it if possible, and report the exact command and output summary. Do not run destructive operations against a production database. Clearly label checks that are unavailable or skipped.
