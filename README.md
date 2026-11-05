# Odoo Claude Code Skills

A Claude Code plugin for developing, installing, testing, debugging, reviewing, and migrating Odoo custom modules. It combines focused Odoo skills with a practical workflow: understand the request, inspect the repo, plan proportionally, test meaningful behavior, investigate failures from evidence, and verify before reporting completion.

## Install

In Claude Code, add this repository as a marketplace and install the plugin:

```text
/plugin marketplace add shone-navabrind/odoo-claude-code-skills
/plugin install odoo-claude-code-skills@odoo-claude-code-skills
```

Or clone the repository and load it for a session with `claude --plugin-dir ./odoo-claude-code-skills`. Check `/help` for installed commands and available skills. Refer to the current Claude Code plugin documentation for installation behavior, which can evolve.

## Commands

- `/odoo-plan` — clarify and plan a feature or refactor before implementation.
- `/odoo-new-module` — build or extend an addon using the detected project conventions.
- `/odoo-review` — review code, security, compatibility, and tests without editing by default.
- `/odoo-install` — diagnose or perform a safe module install/update in a confirmed development/test environment.
- `/odoo-test` — select and run the narrowest relevant tests/checks.
- `/odoo-debug` — investigate an exception or symptom before proposing a root-cause fix.
- `/odoo-migrate` — prepare and perform a source-backed version migration.

## Workflow approach

The design takes general workflow inspiration from the public [obra/superpowers project](https://github.com/obra/superpowers): small reusable skills, explicit planning for non-trivial work, systematic debugging, and verification before completion. It does not copy Superpowers' text or assert that Claude Code can technically enforce every instruction as a hard gate. Read the relevant skill and adapt the workflow to the task.

The Odoo-specific guidance prioritizes version and repository inspection, minimal targeted changes, tests for behavior, security and data safety, and reporting exact checks. Test-first is preferred for behavior changes when a meaningful test can be written and run; when the environment cannot run Odoo tests, do not fake a red/green cycle—state the limitation and use available static or isolated checks.

## Odoo source and version policy

Use official, version-matched Odoo sources for implementation details. Confirm that documentation/source pages exist and apply to the requested release; do not infer a breaking change from a URL or search result alone. The migration skill separates custom-addon code porting from database upgrades. Use Odoo's supported database upgrade process for real database upgrades and validate a test copy before production.

Starting points:

- [Odoo documentation portal](https://www.odoo.com/documentation/)
- [Odoo Community source repository](https://github.com/odoo/odoo)
- [Odoo upgrade utilities](https://github.com/odoo/upgrade-util)
- [Odoo upgrade service](https://www.odoo.com/upgrade)
- [Claude Code plugins documentation](https://code.claude.com/docs/en/plugins)
- [Superpowers repository](https://github.com/obra/superpowers)

Community source does not establish Enterprise behavior. Third-party articles may be research leads but are not sole authority for version-specific code changes.

## Skills

Skills cover module development, ORM, views, security, data/assets, install/update, testing, systematic debugging, migration, and verification. Each skill should be loaded only when relevant, and the specialist source should be inspected when a version-dependent detail is uncertain.

## Contributing

Keep skill descriptions discoverable and workflows actionable. Cite official sources for version-dependent guidance, preserve uncertainty, and avoid speculative migrations. Validate plugin manifests, Markdown, commands, and links before submitting.

## License

MIT. See [LICENSE](LICENSE).
