# Any-version Odoo migration: operational playbook

This is a step-by-step playbook for migrations between arbitrary **requested** versions. “Any version” means the plugin will analyze any source/target pair; it does **not** mean Odoo supports a direct database jump between every pair. Confirm the current supported route first.

## A. Decide the job in plain language

Ask whether the user wants (1) source code adapted, (2) a business database upgraded, or (3) both. Explain briefly: code porting changes addon files; database upgrading transforms an existing database and its data using an approved version path. Then collect only missing source/target versions, edition/hosting, and scope.

## B. Establish facts and protections

1. Inspect repo instructions, Git status, Odoo source/branch, manifests, addon paths, config/scripts/container files, test commands, and custom changes.
2. Identify edition, hosting, installed modules, database/filestore context, integrations, and test environment when available. Do not expose credentials or dump personal data.
3. Do not submit a database or run production changes until user authorizes the exact action and a restorable backup/rollback plan exists.
4. Create an inventory from [migration-inventory.md](migration-inventory.md), grouping first-party, third-party, and unknown-origin addons and dependencies.

## C. Determine database route before touching data

1. Open Odoo's current upgrade docs and service portal; choose exact versions and edition/hosting.
2. Confirm eligibility, direct vs sequential route, intermediate versions, required source/target builds, and current submission/retrieval method. Save exact references and date/version checked.
3. If Odoo's official material does not answer the specific route, label it unknown and pause database execution. Ask Odoo or ask the user whether to evaluate community OpenUpgrade as a separate, explicitly non-Odoo-supported option.
4. Do not trust old CLI examples or search snippets. Inspect current official command help. Never execute `curl | sh`, download-and-run a remote script, transmit dumps, or trigger production from the agent without explicit user consent.

## D. Port addons, dependency order, one at a time

For each addon in dependency order:

1. Inspect its manifest, full relevant code, tests, XML IDs, security, assets, data, and existing migrations.
2. Establish provenance. For third-party code, request permission for online lookup; check publisher/repo, license, target branch/release, and compatibility evidence. Offer two clear choices: use compatible upstream release, or locally port current source. Avoid replacing custom forks silently.
3. Compare only used APIs and syntax against source/target official docs and exact official source branches. Record a finding only when the target incompatibility is evidenced and this addon uses it.
4. Fix specific parser/syntax errors based on actual target Python/Odoo requirement and traceback. Fix framework/API changes by comparing definitions and call sites. Fix XML errors using target view definitions, IDs, dependency order, and XPath validation. Keep edits minimal.
5. Decide whether data transformation is needed. If so, follow target-version official custom upgrade-script docs for exact directory layout, version naming, phase, signature, and utility API. Add tests for data preservation.
6. Run syntax/static checks and the narrowest target Odoo tests. On disposable DB, install/update the addon and validate behavior/security. Record exact commands and results.
7. Update inventory and summarize; ask “Continue to the next addon?” unless user has clearly authorized processing all addons. Do not proceed past a blocked dependency without explaining.

## E. Database upgrade test cycle

After addon code and dependencies are target-ready, and only if database upgrade was requested:

1. Back up database and filestore; verify restore to an isolated environment.
2. Create protected test copy and follow Odoo's currently supported test upgrade submission/retrieval procedure for the specific deployment.
3. Start upgraded DB with matching target Odoo code, configuration, and addon paths. Capture complete logs and avoid repeated attempts against the only copy.
4. Verify database/module state, data invariants and relations, companies, user access, attachments/filestore, integrations, reports, scheduled tasks, and business-critical workflows.
5. Fix issues in the relevant addon/script, rebuild test copy, repeat. Keep database-path failures separate from addon-test failures.
6. Provide a go/no-go report. Production is a distinct, explicit user-approved operation with downtime, backup/restore, and rollback plan.

## F. Source authority and tool categories

- **Official Odoo:** versioned Odoo documentation, Odoo source branches, Odoo upgrade service, and official upgrade-util repository. Use only after checking exact applicability.
- **Community:** OCA OpenUpgrade and third-party addons/articles. Useful options/leads, but not official Odoo service or support. Label clearly and get user direction before adopting.
- **Private/Enterprise:** Community source/docs cannot establish behavior for private Enterprise addons. State access gaps.

## G. Completion criteria

Do not say “migration complete” unless the requested scope is complete and verified. State separately: addon code status; each module's target test/install status; database test-upgrade status; production status. Include unresolved claims, source links, exact checks, backup/rollback status, and next user decision.
