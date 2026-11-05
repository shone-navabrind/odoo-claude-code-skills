---
name: odoo-migration
description: Plan or perform an Odoo addon-code migration, a database version upgrade, or both, between any requested source and target versions. Use when upgrading Odoo, porting custom or third-party addons, writing upgrade scripts, or assessing a database migration. Always establish exact versions/edition/hosting, verify the supported path from current official sources, and work one addon at a time.
---

# Odoo migration: any source version to any target version

This skill covers **code migration**, **database upgrade planning**, and **per-addon migration scripts**, which are related but distinct. A custom-module code port does not upgrade a database. An Odoo database upgrade does not automatically make every custom or third-party addon compatible. Never imply that arbitrary source-to-target database jumps are supported; prove the route from current Odoo guidance.

## 0. Start with a simple scope check

Explain in plain language what the user wants:

- **Code only:** adapt addon source so it works on the target Odoo version; no database conversion.
- **Database only:** upgrade a database using an approved path; custom addons still need compatible code.
- **Both:** port addons, then test the Odoo database upgrade and addon behavior together.

Ask only questions that change the migration plan. Gather:

1. Source version and target version (if not detectable).
2. Community or Enterprise; Odoo Online, Odoo.sh, or self-hosted.
3. Whether a real database with business data must be upgraded or only source code.
4. Addon repository/path and whether the user wants one addon first or the full dependency set.
5. For third-party addons: ask in simple terms: **“These addons come from outside your team. Should I check online for a compatible target-version release, or should I port the current code ourselves?”** Do not upload private code/data or contact maintainers without permission.

If the repository provides reliable version evidence, state it and ask only for missing high-impact details. Do not interrogate the user for facts already discoverable locally.

## 1. Freeze facts and make a migration inventory

Before editing:

- Detect Odoo version from source branch/runtime/config/manifest conventions, and cross-check with the user's input. Record commit/tag, edition, Python/PostgreSQL environment only when actually verified.
- Inspect repository instructions, addon paths, lockfiles/container config, CI, module manifests, migrations, tests, and current local changes. Preserve unrelated work.
- Build the addon dependency graph using each `__manifest__.py` `depends` field. List core, first-party custom, and third-party addons separately. Mark unknown provenance as `unknown`, not third-party fact.
- Record per addon: technical name, source location, provenance, source version, target availability, dependencies, install state if known, upgrade scripts, test coverage, and status.
- Find actual version-sensitive usage with targeted searches: imports, overrides, model/field/method references, XML view inheritance, security, assets/frontend, controllers/RPC, data and tests. Do not perform broad edits from a generic checklist.

Use [migration inventory template](../../docs/migration-inventory.md). Do not begin a mass edit across every addon.

## 2. Establish the official database path (do not guess)

For database work, use the documentation matching the source and target, and check the current Odoo upgrade service guidance for the database's edition, hosting, and versions. Record links and exact statements. Confirm:

- Is this source database eligible for the requested destination?
- Is a direct jump supported, or must the database go through sequential intermediate versions?
- Which tool/service is official for the hosting and edition?
- What dump/filestore, access, size, downtime, and test-upgrade prerequisites apply?
- Are there target runtime and custom-module requirements?

Use Odoo's official upgrade service/process where applicable. The submission/CLI interface may change; **read the current official instructions and command help immediately before use**. Do not execute a remote script fetched with `curl | sh`, submit a database, or initiate a production upgrade automatically. Show what will be sent, where, and whether it is test or production; require explicit user confirmation before transmitting data or taking an irreversible/production action. Protect database dumps, filestore, credentials, and personal data.

If official support/path cannot be verified, stop before a database conversion and explain the gap. Offer options: obtain confirmation from Odoo, use a verified intermediate path, or discuss community tooling. Do not silently substitute OpenUpgrade. Label [OCA OpenUpgrade](https://github.com/OCA/OpenUpgrade) as community-maintained and ask permission before selecting it.

## 3. Plan the sequence and checkpoints

Present a concise plan before substantial edits:

1. Inventory and confirm source/target facts and official DB route.
2. Resolve dependency order; select **one addon** and its required dependencies.
3. Check official target-version documentation/source and third-party availability for that addon.
4. Port only confirmed incompatibilities and syntax/API changes in that addon; preserve behavior.
5. Run syntax/static checks, focused tests, and install/update on disposable target-version DB.
6. Record results and unresolved issues; get user approval to continue to the next addon.
7. After all addon code is compatible, run a test database upgrade through the approved route, validate data/business workflows, repeat fixes, then schedule production only with explicit approval/backups.

For a large addon set, create a progress table and keep each addon's status independent: `not started`, `researching`, `ported`, `tests passed`, `blocked`, `unverified`.

## 4. Research and port one addon at a time

For the selected addon:

1. Confirm upstream provenance. For third-party code, check official publisher/repository/release metadata and target branch if online research is authorized. Report repository/maintainer, license/access caveats, target-version availability, and evidence. Ask whether to use that version or locally port. Never overwrite local custom changes with upstream source without review.
2. Read source and target official developer docs for relevant APIs, official release notes, and exact `odoo/odoo` branch code. Consult Enterprise sources only if authorized/available; Community source cannot prove Enterprise behavior.
3. Maintain an evidence ledger: finding; source URL/path/commit; affected file/line; status (`confirmed`, `not applicable`, `unverified`); minimal change; test.
4. Diagnose syntax compatibility precisely: parser/compiler error first; identify syntax/runtime or framework API incompatibility; compare target Python/Odoo requirements from official version docs; edit the smallest affected construct; run parser/compile/lint and targeted runtime test. Do not mechanically rewrite syntax based only on version labels.
5. For ORM changes, compare actual field/method definitions, override signatures, compute/inverse/search dependencies, access behavior, and callers between versions. For XML, verify target view architecture, referenced external IDs, XPath nodes, modifiers, load order, and assets. For security, preserve least privilege and test both allow/deny paths.
6. Keep unrelated refactors out of the migration. Add regression tests for observable behavior and any transformed data.
7. Update the inventory only after tests and review. Report exact changed files, commands/results, and remaining unknowns, then ask simply: **“This addon is ported and checked. Continue with the next addon?”** unless the user already authorized a batch.

## 5. Addon upgrade scripts and data transformations

A code port and a data transformation are different. First inspect the target release's official upgrade-script documentation and local addon conventions. Verify exact directory names, version naming, execution phase, function signature, API, and triggering conditions for that Odoo version; these can change. Odoo documentation commonly describes per-module upgrade scripts and `migrate(cr, version)`, but do not assume paths or lifecycle without checking the target docs.

When a schema/data change requires a script:

- State the invariant: what business meaning and references must remain true.
- Choose the documented phase (`pre`, `post`, or `end`) based on whether old schema, new schema, or all module updates are needed.
- Make script narrowly scoped, safe for the actual upgrade lifecycle, and idempotent where the framework expects/retries it. Use documented upgrade utilities where applicable; direct SQL only with parameterized statements, clear constraints, and review.
- Test on a database copy with representative records, nulls, relations, companies, and large-data considerations. Verify counts, relations, values, and repeat/recovery behavior. Do not run migration scripts on production during development.
- Keep module version metadata and upgrade-script folder naming aligned with the actual release docs. Never invent a migration directory convention from memory.

## 6. Database upgrade execution and validation

Only after code and route are established:

1. Securely create and verify a restorable database backup and corresponding filestore backup; test restore to a separate environment.
2. Freeze writes/developments as required by the official process; record source DB, version, edition, installed modules, custom addons, integrations, and target.
3. Make a sanitized or appropriately protected test copy. Use the official test-upgrade flow first; comply with data privacy/security requirements.
4. Apply any required custom module preparation exactly as the official docs specify. Do not assume the upgrade service accepts arbitrary custom modules or that locally installed code is automatically included.
5. Follow the currently documented official command/UI for submission and retrieval. Confirm target and test mode; do not infer CLI flags or pipe a remote script into a shell.
6. Start the upgraded test DB with matching target Odoo source and addon paths. Review complete logs; resolve one root cause at a time.
7. Validate installed module states, schema/data invariants, record counts, company boundaries, scheduled jobs, reports, integrations, and user-critical workflows. Run targeted tests and module install/update checks in disposable copies.
8. Repeat test upgrades until blockers are resolved. Produce a go/no-go report, remaining-risk list, rollback plan, downtime plan, and exact production steps.
9. Production upgrade is a separate user-approved operation. Never initiate it without explicit confirmation and a verified recovery plan.

## 7. Required final report

Include:

- source/target version, edition, hosting, and what was verified;
- official DB path and source links, or the precise reason it remains unknown;
- addon inventory summary, provenance (first-party/third-party/unknown), and per-addon statuses;
- third-party compatibility findings and user's choice (upstream target release vs local port);
- code changes and data scripts, each linked to evidence;
- checks actually run and exact outcomes; separate code tests from DB upgrade validation;
- unresolved/unsupported changes and risks;
- next decision in plain language.

Never claim all versions are mutually compatible, claim a database is upgraded because code compiles, or describe community tooling as official Odoo tooling.
