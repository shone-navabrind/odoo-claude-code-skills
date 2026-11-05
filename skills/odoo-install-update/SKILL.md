---
name: odoo-install-update
 description: Install or update Odoo addons, configure development addon paths, and diagnose module loading and registry errors safely.
---

# Odoo addon installation and update

Use when setting up a development environment, installing/updating a module, or diagnosing discovery, dependency, loading, or registry problems. Exact options vary; inspect the checked-out Odoo version and `./odoo-bin --help` before relying on CLI details.

## Safety and environment check

1. Confirm the target database is disposable/development/test, not production. Identify Odoo checkout/entrypoint, config, database, addon paths, module technical name, and version.
2. Do not expose passwords, tokens, database URLs, or private config contents in output. Avoid destructive database operations; request confirmation before any irreversible action.
3. Check whether PostgreSQL and the selected database are reachable with the project's configured method. Do not assume database names, ports, service names, or container layout.
4. Verify the module directory is on an effective addons path; inspect `addons_path` in the active config/command, module technical name (directory name), manifest validity, and Python package imports.
5. Check every declared dependency is available for this edition/version and its addon path is visible. Enterprise-only dependencies require the appropriate source and entitlement; don't substitute a similarly named module blindly.

## Install/update workflow

- Prefer the repository's documented Docker/devcontainer/Makefile/CI command if present. Inspect it before invoking.
- Otherwise consult the exact Odoo version's CLI help and official documentation. Common Odoo CLI forms include `-i <module>` for installation and `-u <module>` for module updates, with a selected database (`-d <database>`); confirm flags and behavior in the installed version before use.
- Run against a test database or disposable copy. Use `--stop-after-init` only when appropriate for the deployment mode and verify its version-specific semantics.
- Capture stdout/stderr and the Odoo log. Verify process exit status, module state, registry startup, view validation, and intended UI/business behavior.
- For automated tests, choose an appropriate test enablement/filter and stop behavior from that version's CLI help and test docs. Do not combine assumptions from unrelated releases.

## Common discovery/install failure checks

- Module not found: addon path, technical directory name, config actually loaded, process restart/Apps list refresh as appropriate, container mount, permissions.
- Missing dependency: manifest dependency spelling/version/edition and whether dependency addons path is mounted.
- Python import/registry failure: syntax/import chain, package `__init__.py`, unavailable dependency, model override/signature compatibility.
- XML parse/external ID/view validation error: read the first concrete failing record and file; check XML syntax, dependency/load order, external IDs, model fields, view inheritance target and target-version syntax.
- Access/data load failure: CSV headers and IDs, group/model references, access/rule semantics, `noupdate`, and load order.
- Update appears ineffective: confirm correct database, process/config, module technical name, source path mounted, update command exit status, and whether the relevant file is loaded by the manifest.

Do not repeatedly retry a failing upgrade on a valuable database. Preserve logs, restore a known-good copy if needed, repair and validate on a clone first, then follow the approved upgrade procedure.
