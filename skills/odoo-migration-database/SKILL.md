---
name: odoo-migration-database
 description: Plan and validate an Odoo business database upgrade across requested versions, including route discovery, backup, test-upgrade cycles, custom module readiness, and production safety.
---

# Odoo database migration

Read `../../docs/migration-any-version.md` for the operational sequence and `../../docs/migration-inventory.md` for tracking. Use this skill only when an existing database must be upgraded. For source-only addon changes, use `odoo-migration` code-port steps instead.

## Step-by-step

1. Establish source/target versions, edition, hosting, database and filestore scope, and whether target is test or production. Never put credentials or sensitive dumps into chat.
2. Consult current official Odoo upgrade docs/service for that exact combination. Record direct/sequential route, intermediate versions, eligibility, and current official submission/command procedure. Do not assume a direct jump or reuse old CLI syntax.
3. If route is unclear, stop before conversion and ask the user to confirm with Odoo or authorize evaluation of community alternatives. Clearly mark OCA OpenUpgrade as non-Odoo community tooling.
4. Inventory installed modules, dependencies, custom/third-party provenance, integrations, and target-compatible code. Use addon inventory skill; resolve target availability for third-party addons with user permission.
5. Require a verified restorable database and filestore backup. Restore a copy to an isolated test environment before testing. Do not initiate production, submit dumps, or run network-upgrade commands without explicit confirmation of action, target, data handling, and environment.
6. Follow the current official test-upgrade workflow exactly. Do not compose commands from memory. Capture logs, exit status, target version, and tool/service outcome.
7. Start the result under matching target source/addons. Validate schema/data invariants, module states, access/company boundaries, attachments, reports, integrations, scheduled work, and user-critical workflows.
8. Diagnose failures via full logs and relevant addon; fix code/data scripts minimally, then repeat against a fresh copy as required by the upgrade method.
9. Deliver separate statuses: test database upgrade, addon compatibility, business validation, and production. Provide go/no-go, downtime, rollback and remaining-risk notes. Production requires explicit separate approval.

A successful database conversion is not proof every custom workflow is correct. A module that installs on an empty database is not proof existing data migrated correctly.
