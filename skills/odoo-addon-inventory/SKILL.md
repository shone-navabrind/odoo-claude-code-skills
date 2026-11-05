---
name: odoo-addon-inventory
description: Inventory Odoo addons and dependencies before migration or repository changes, identify third-party modules and upstream compatibility, and create a one-addon-at-a-time work plan. Use before large migrations or when addon ownership/availability is unclear.
---

# Odoo addon inventory and provenance

Read `../../docs/migration-inventory.md` when preparing a migration. Keep exploration efficient and specific to the requested addon scope.

1. Find addon roots from repository documentation/config, `addons_path`, containers, CI, and directory structure. Do not assume a single `addons/` path.
2. Read each relevant `__manifest__.py`; extract technical name, dependencies, version/license/author/website if present. Treat metadata as clues, not proof of ownership.
3. Classify origins using repository remotes, directory provenance, vendoring/submodule info, license headers, and maintainer metadata: first-party, third-party, or unknown. Cite evidence and do not call unknown-origin code third-party as fact.
4. Build dependency order and flag unavailable or edition-specific dependencies. Keep a custom fork distinct from its upstream module.
5. For third-party addons, ask whether online lookup is allowed. If allowed, use the publisher's official repository/release information where possible; record target branch/tag, evidence date, license/access, and differences from local fork. Do not assume a similarly named module is compatible.
6. Present simple user choices: compatible upstream target release (if verified) or local port of the current code. Explain implications without jargon and wait for the user's direction if choice materially changes ownership/behavior.
7. Process each addon as an isolated unit; update status and ask whether to continue unless a batch was explicitly requested.

Never download or overwrite addon source, contact maintainers, transmit private source, or accept a license without permission.
