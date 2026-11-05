# Odoo Claude Code Skills

A Claude Code plugin for building and maintaining Odoo custom modules, with focused skills for the ORM, views, access control, data, tests, and version migrations. The migration workflow is deliberately evidence-first: it does not invent version changes or treat unverified blog posts as authoritative.

## Install

From Claude Code, add this GitHub repository as a marketplace and install the plugin:

```text
/plugin marketplace add shone-navabrind/odoo-claude-code-skills
/plugin install odoo-claude-code-skills@odoo-claude-code-skills
```

Alternatively, clone this repository and load it for a session with `claude --plugin-dir ./odoo-claude-code-skills`.

Restart/reload Claude Code if needed, then use `/help` to see available commands and invoke skills by their names/descriptions.

## Commands

- `/odoo-new-module` — scaffold a module based on this repository's conventions and requirements.
- `/odoo-review` — inspect a module for correctness, security, maintainability, and tests.
- `/odoo-migrate` — plan and perform a source-backed version migration.
- `/odoo-test` — identify the narrow relevant test command and test scope.
- `/odoo-debug` — trace an Odoo error from evidence in the traceback and code.

## Skills

Skills cover end-to-end module development, ORM/model design, XML views and UI, security, data/assets, testing, and migrations. Use only the specialist guidance relevant to the task. Skills instruct Claude to inspect the checked-out project and installed Odoo version before changing code, preserve local conventions, minimize unrelated edits, and report checks actually run.

## Migration safety

The migration skill does not claim that a release has particular breaking changes without authoritative evidence. It checks the source/target versions, official Odoo documentation and upgrade guidance, and—when available—the relevant official Odoo source branches and upgrade scripts. Every proposed change should be tied to a confirmed source or a concrete incompatibility in the module. If Odoo's official target-version material is missing or inconclusive, the plugin says so and asks for evidence or treats the point as unresolved rather than guessing.

Official starting points:

- [Odoo documentation](https://www.odoo.com/documentation/)
- [Odoo upgrade documentation](https://www.odoo.com/documentation/19.0/administration/upgrade.html) (select the actual target version's documentation where available)
- [Odoo source repository](https://github.com/odoo/odoo)
- [Odoo upgrade-util](https://github.com/odoo/upgrade-util)

Official documentation pages are versioned and may change. Always use pages and source branches matching the actual source and target releases. Odoo Enterprise source is not fully public; do not infer Enterprise internals from Community source alone.

## Repository layout

- `.claude-plugin/` — plugin and marketplace manifests.
- `skills/<skill-name>/SKILL.md` — automatically discovered skill instructions.
- `commands/*.md` — user-invocable slash commands.
- `docs/` — concise source-of-truth pointers and migration workflow notes.

## Contributing

Keep guidance actionable and version-aware. Prefer official Odoo and Anthropic documentation; label uncertainty and avoid turning conjecture into migration instructions. Validate Markdown, JSON, plugin discovery, and examples before submitting changes.

## License

MIT. See [LICENSE](LICENSE).
