---
name: odoo-data-assets
description: Work with Odoo manifests, XML/CSV data, demo data, assets, translations, and module installation/update behavior.
---

# Odoo module data and assets

Inspect the manifest and target-version examples in the repository before modifying load order, asset bundles, or data semantics.

## Manifest and data

- Keep `depends`, `data`, `demo`, assets, version, license, and installability accurate and minimal.
- Ensure dependencies provide every referenced model and external ID; data files load in dependency order.
- Use stable XML IDs and preserve references when editing records.
- Distinguish `noupdate` records from records intentionally refreshed on module update; understand the consequences before changing it.
- Make install/update data safe to rerun. Avoid duplicate records and destructive hooks.
- For CSV security/data, verify headers, model external IDs, group IDs, and load order.
- Keep demo data out of production data declarations.

## Assets and translations

- Follow asset registration syntax and bundle names from the exact target version and local addon patterns.
- Avoid modifying compiled output or generated bundles.
- Preserve translation extraction conventions and user-visible strings.
- Test a clean install and module upgrade when relevant; inspect server/browser logs for missing assets or invalid XML.

Data migrations that transform existing business records require explicit preservation/rollback considerations, tests on a copy, and a documented source/target upgrade path. Do not perform destructive data operations speculatively.
