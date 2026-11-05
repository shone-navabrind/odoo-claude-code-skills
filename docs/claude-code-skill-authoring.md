# Claude Code plugin and skill authoring notes

This plugin uses small, relevant skills and linked detailed references so common tasks do not pull every migration detail into context. Verify the current official docs before changing packaging because Claude Code evolves.

## Authoring rules used here

- Plugin metadata lives in `.claude-plugin/plugin.json`; marketplace metadata is separate. Skills and commands live in their standard plugin-root directories.
- A skill is `skills/<skill-name>/SKILL.md` with YAML frontmatter. Keep frontmatter valid and minimal; `name` and a discoverable `description` are key. The description should say what it does and when to use it, including likely user phrasing.
- Put actionable core workflow in `SKILL.md`; move long checklists/templates/reference material to linked `docs/` or skill-local references. Tell Claude explicitly when to open those files.
- Keep instructions concrete and scoped. Prefer a small workflow, decision points, pitfalls, and output expectations over vague “be thorough” language.
- Do not claim a markdown skill creates a hard gate, invokes a tool automatically, or guarantees behavior. Skills guide the model; hooks/commands are separate mechanisms and should be added only with a specific validated need.
- Slash command markdown should state when it applies, relevant skill, what context to inspect, safety boundaries, and expected output. Do not include outdated command syntax as authoritative.
- Check whether a skill is discoverable and invoked appropriately; check that it does not over-trigger or load unrelated references. Test plugin structure with current Claude Code validation tooling when available.

## References

- [Claude Code plugins](https://code.claude.com/docs/en/plugins)
- [Plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code skills](https://code.claude.com/docs/en/skills)
- [Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- [Public Superpowers project](https://github.com/obra/superpowers) — workflow inspiration only; this project does not copy its content.

## Review checklist for a skill change

1. Does the description identify correct triggers and avoid unrelated triggers?
2. Is every task instruction actionable and version-aware?
3. Are safety, uncertainty, and tool limitations explicit?
4. Are long details placed in linked docs and loaded only when relevant?
5. Are examples accurate for the named Odoo version, or labeled illustrative?
6. Did a real reader/test verify the skill remains understandable and non-contradictory?
