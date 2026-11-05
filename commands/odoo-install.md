---
description: Diagnose and, when requested, safely install or update an Odoo module in a development or test environment.
argument-hint: [module technical name, database/environment, and install or update]
---

Use the `odoo-install-update` skill. Inspect project scripts/config and the installed Odoo version's CLI help first. Confirm the target is not production and identify the database, addon path, module technical name, and requested action before running a command. Do not expose credentials or run destructive operations without explicit authorization. Explain the command and expected effect, capture its exit status/logs, and verify the resulting module behavior. If context is incomplete, diagnose or propose a command rather than executing an unsafe guess.
