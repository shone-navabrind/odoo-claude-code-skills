# Odoo Claude Code Skills

A Claude Code plugin for developing, installing, testing, debugging, reviewing, and migrating Odoo custom modules. It supports migrations between **any requested source and target versions** by inspecting the actual versions and evidence; it does not pretend every arbitrary jump is a supported one-step database upgrade. The workflow distinguishes addon code porting from database migration and handles one addon at a time.

## Install

In Claude Code, add this repository as a marketplace and install the plugin:

```text
/plugin marketplace add shone-navabrind/odoo-claude-code-skills
/plugin install odoo-claude-code-skills@odoo-claude-code-skills
```

Or clone the repository and load it for a session with `claude --plugin-dir ./odoo-claude-code-skills`. Check `/help` for installed commands and skills. Plugin installation syntax and discovery behavior can change; consult current Claude Code documentation if needed.

## Commands

- `/odoo-plan` — clarify and plan a feature/refactor in plain language before implementation.
- `/odoo-new-module` — build or extend an addon using detected project conventions.
- `/odoo-review` — review code, security, compatibility, third-party dependencies, and tests.
- `/odoo-install` — diagnose or perform a safe module install/update in a confirmed development/test environment.
- `/odoo-test` — select and run the narrowest relevant tests/checks.
- `/odoo-debug` — investigate an exception or symptom before proposing a root-cause fix.
- `/odoo-migrate` — plan and execute addon-code and/or database upgrade work for the requested versions, with evidence and user checkpoints.

## Migration scope

The plugin can analyze and guide migrations from any source version to any target version, but supported database paths, required intermediate hops, runtimes, and available scripts depend on Odoo's currently published support for those exact releases and the database edition/hosting. It never silently assumes an arbitrary direct database jump is supported. It identifies the path using current official Odoo material; if this is unavailable, it clearly distinguishes verified facts from unknowns and asks before choosing a community route.

The migration process is documented in [docs/migration-any-version.md](docs/migration-any-version.md) and [skills/odoo-migration/SKILL.md](skills/odoo-migration/SKILL.md). It inventories addons and dependencies, labels third-party modules, asks whether to research compatibility online or port locally, migrates one addon at a time, and treats database upgrade, addon code port, and per-module data scripts as separate workstreams.

## Workflow approach

The design takes general workflow inspiration from the public [obra/superpowers project](https://github.com/obra/superpowers): reusable focused skills, planning proportional to risk, systematic debugging, test-first where feasible, and verification before completion. It does not copy Superpowers' text or claim instructions are technically hard-enforced. Current Claude Code plugin/skill behavior is documented at [plugins](https://code.claude.com/docs/en/plugins), [skills](https://code.claude.com/docs/en/skills), and [skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices).

## Official Odoo starting points

- [Odoo documentation portal](https://www.odoo.com/documentation/) — select the exact version.
- [Odoo Community source repository](https://github.com/odoo/odoo) — inspect the exact release branch/tag.
- [Odoo upgrade service](https://www.odoo.com/upgrade) and [upgrade service portal](https://upgrade.odoo.com/) — verify current eligibility, paths, and submission procedure.
- [Odoo upgrade utilities](https://github.com/odoo/upgrade-util) — inspect tool documentation and exact applicability.
- [Claude Code plugin marketplace docs](https://code.claude.com/docs/en/plugin-marketplaces).

[OCA OpenUpgrade](https://github.com/OCA/OpenUpgrade) is a **community project, not Odoo S.A.'s official upgrade service**. The plugin must label it accordingly and ask before adopting it.

## Skills

Focused skills cover module development, ORM, views, security, data/assets, install/update, test-first development, testing, systematic debugging, code review, verification, feature planning, and migration. Main skill files stay concise and point to detailed references for progressive disclosure.

## License

MIT. See [LICENSE](LICENSE).
