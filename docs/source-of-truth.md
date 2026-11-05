# Source pointers and version policy

Use this page to avoid rediscovering the same primary references. Open only the pages that bear on the task and verify that they match the installed/source and target versions.

## Official Odoo sources

- Documentation index: https://www.odoo.com/documentation/
- Developer documentation (select the version matching the checkout): https://www.odoo.com/documentation/19.0/developer.html
- Upgrade documentation (select the version matching the target): https://www.odoo.com/documentation/19.0/administration/upgrade.html
- Official Community source: https://github.com/odoo/odoo
- Odoo upgrade utilities: https://github.com/odoo/upgrade-util
- Official upgrade service information: https://www.odoo.com/upgrade

The `19.0` URLs above are examples of versioned documentation paths, not a claim that every target-specific page exists or that its content applies to another release. Navigate to the actual version in use. For technical breaking changes, inspect official versioned documentation, official release notes, official source history, and applicable upgrade scripts. Treat each as evidence for a specific claim.

## Evidence rules

1. Record source version, target version, edition (Community/Enterprise), hosting/deployment context, and module dependencies.
2. Prefer official Odoo documentation and source. Third-party articles are leads only, never sole evidence for a code change.
3. Cite each version-specific finding with exact page, source path/commit, or migration script and explain its impact on the module.
4. A changed implementation in a source branch is not automatically a supported API change. Establish that the custom module depends on it.
5. Do not copy Enterprise-specific assumptions into Community modules. Enterprise source and upgrade details may not be public.
6. If the official target release's guidance is absent, mark the finding `UNVERIFIED`; do not fabricate replacement APIs, removed models, environment requirements, or upgrade steps.
7. Use Odoo's supported database upgrade process for database upgrades. Porting custom module code is a separate task and does not itself migrate a production database.

## Claude Code references

- Plugin structure and manifest: https://code.claude.com/docs/en/plugins
- Plugin manifest reference: https://code.claude.com/docs/en/plugins/manifest-reference
- Skills: https://code.claude.com/docs/en/skills
