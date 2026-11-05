---
name: odoo-migration-script-authoring
description: Design, implement, and test Odoo custom addon pre/post/end upgrade scripts and data transformations using the exact target version's documented conventions.
---

# Custom addon upgrade-script authoring

Before writing a script, inspect the target release's official upgrade-script docs and local code. Open `../../docs/migration-any-version.md` for the broader migration process. Do not rely on remembered paths, lifecycle, signatures, or utility APIs.

## Procedure

1. Describe the data/schema change and invariant in plain language. Identify source schema, target schema, relations, company scope, existing records, and rollback/retry considerations.
2. Find exact target-version official documentation for script directory naming, module-version trigger, phase (`pre`, `post`, `end`), filename, `migrate` signature, cursor/environment, and utility library. Cite the applicable page/branch.
3. Choose phase by data dependencies: old schema needed before update, new schema needed after module update, or all module updates needed before end phase—verify semantics in docs.
4. Implement only necessary transformation. Prefer documented upgrade utilities where applicable. If SQL is needed, parameterize values, scope rows explicitly, preserve references, and avoid unsafe broad updates/deletes.
5. Handle nulls, duplicate keys, existing target records, large tables, multi-company relationships, and rerun/failure behavior as relevant. Don't claim idempotence unless designed and tested.
6. Add focused tests or a migration harness using representative old-version data. Run only on a disposable DB copy; prove record counts, relations, values, and business invariants.
7. Verify script is discovered/executed under the actual module version transition and target process. Report exact setup and checks; don't claim test DB upgrade based only on syntax compilation.

Keep custom-addon scripts distinct from Odoo core/official upgrade service scripts and from OCA OpenUpgrade scripts. They are not interchangeable without explicit technical evidence.
