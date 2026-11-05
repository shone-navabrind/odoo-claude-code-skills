---
name: odoo-migration
description: Migrate Odoo custom modules between major or minor versions, analyze version compatibility, and plan database-safe upgrade work.
---

# Odoo module migration

This skill ports custom module code and helps plan validation; it does not replace Odoo's supported database upgrade service/process. Never invent release notes or breaking changes.

## Inputs to establish

- Source and target Odoo versions/branches.
- Community or Enterprise, hosting/deployment type, installed apps and dependencies.
- Whether the request is code-only, database upgrade, or both.
- Repository/addon paths, available target source/runtime, representative customizations and test data.

If essential, ask one focused question. Otherwise state assumptions and proceed with an evidence inventory.

## Evidence-first workflow

1. Inspect module manifests, code, tests, XML IDs, dependencies, assets, security, and custom data/migration scripts. Build a targeted inventory of framework APIs actually used.
2. Consult `docs/source-of-truth.md` and the relevant official source-version and target-version documentation, release notes, Odoo source branches, and upgrade utilities. Verify target sources exist and match the requested release.
3. Compare only relevant APIs and structures. For each suspected incompatibility, capture authoritative evidence and exact affected file/line. Third-party migration articles may suggest search terms, but cannot justify a change by themselves.
4. Classify each item `confirmed`, `not applicable`, or `unverified`. Do not change unverified items. Do not claim a model/API was removed or an environment prerequisite changed without direct official evidence.
5. Port minimally, preserving data meaning, access policy, public interfaces, and idempotence. Separate code compatibility changes from database transformation and operational upgrade steps.
6. Add regression tests for changed behavior/data. Test against the target Odoo runtime when available; otherwise clearly identify static-only validation.
7. Use a disposable database copy and Odoo's supported upgrade process for DB validation; verify business-critical workflows and reconcile data before production.
8. Report evidence links, edits, commands/results, unverified risks, and a safe rollout/backup/rollback plan.

## Data migration safeguards

- Understand source schema, target schema, record counts, relations, constraints, and company ownership before transforming data.
- Preserve stable identities/references where required; avoid destructive SQL or broad deletes.
- Migration scripts must be correctly placed/versioned for the actual module convention and target framework; verify transaction and rerun expectations from official guidance/local examples.
- Test on a database copy and prove invariants before recommending production execution.
- Do not confuse Odoo core database upgrade scripts with a custom addon's migration scripts.

For the specific 19.0 → 20.0 workflow, see `docs/odoo-19-to-20.md`. That note intentionally does not assert a breaking-change list: claims must be established from current official 20.0 sources and the actual module.
