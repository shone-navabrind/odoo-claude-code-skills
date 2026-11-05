# Official Odoo development and operations references

These are canonical starting points, not a substitute for checking the exact version. Documentation structure, URLs, CLI flags, test framework details, and APIs can change. Select the version that matches the checkout and verify each page's contents before applying it.

## Official documentation

- [Documentation version selector](https://www.odoo.com/documentation/)
- [Developer documentation landing pages](https://www.odoo.com/documentation/19.0/developer.html) (example version only; navigate to the actual version)
- [Administration documentation](https://www.odoo.com/documentation/19.0/administration.html) (example version only)
- [Upgrade documentation](https://www.odoo.com/documentation/19.0/administration/upgrade.html) (example version only)
- [Odoo upgrade service](https://www.odoo.com/upgrade)

## Official source/tools

- [Odoo Community source](https://github.com/odoo/odoo) — inspect the release branch corresponding to the installed/target version for implementation details.
- [Odoo upgrade-util](https://github.com/odoo/upgrade-util) — inspect its own documentation and scripts; verify applicability to the specific upgrade task.
- [Odoo CLI](https://www.odoo.com/documentation/19.0/developer/reference/cli.html) — example version path; verify current location and exact options for the checkout.

## How to use the references without wasting effort

1. Search the local repository first for its Odoo version, canonical dev command, addon paths, and existing patterns.
2. Use targeted official documentation/source lookups for the API, option, model, view, test, or migration concern at hand, rather than reading the whole docs site.
3. Prefer installed CLI help for the exact executable: `./odoo-bin --help` (or the project/container equivalent). Check the repository's scripts/config before choosing a command.
4. When a docs path redirects, is unavailable, or appears inconsistent with the source version, use the official documentation version selector and mark the unresolved guidance rather than guessing.
5. Treat official source as implementation evidence, not automatically a guarantee of stable public API. Cite the exact version/branch and relevant code path for compatibility conclusions.
6. Use third-party material only as a lead to investigate in primary sources. Do not reproduce an unsupported checklist as fact.

## Related plugin workflows

- [Odoo development workflow](dev-workflow.md)
- [Odoo error triage](error-triage.md)
- [Odoo 19 to 20 evidence policy](odoo-19-to-20.md)
