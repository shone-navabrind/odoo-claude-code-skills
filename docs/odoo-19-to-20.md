# Odoo 19 to 20 migration status and workflow

## Important: do not guess version changes

Odoo releases versioned documentation and source over time. Before using this note, confirm that official 20.0 materials are actually published and inspect their current contents. The presence of a URL, a search result, a third-party checklist, or a proposed change is not proof of an official breaking change. This file intentionally does not list unverified model removals, API changes, Python/PostgreSQL minimums, or other requirements.

## Required verification

For an actual 19.0 → 20.0 task:

1. Confirm the application source really is Odoo 19.0 and the requested target is 20.0; identify Community/Enterprise, hosting, installed modules, and database scope.
2. Check the official [Odoo documentation](https://www.odoo.com/documentation/) for 19.0 and 20.0. Confirm the target pages load and are for the correct release. Read upgrade guidance and relevant developer/framework sections.
3. Check official Odoo 19.0 and 20.0 source branches and relevant commits for the exact APIs/models/views/assets the custom module uses. Record links or commit hashes.
4. Check official upgrade scripts/utilities relevant to any database schema/data change. Do not make a code port stand in for a database upgrade.
5. Search this module for the affected symbols and identify concrete usages. Do not change unrelated code based on a general release note.
6. For every finding, record `confirmed`, `not applicable`, or `unverified`; link the official evidence and state the proposed code/data impact.
7. Implement only confirmed required changes, preserve data semantics, and add/adjust tests. If evidence is insufficient, report the uncertainty and leave the speculative edit unapplied.
8. Run static checks and module tests in the target-version environment when available; provide the exact commands and results. Validate a copy of the database using Odoo's supported upgrade path before production.

## Evidence table template

| Finding | Official evidence (URL/path/commit) | Affected code/data | Status | Action/test |
|---|---|---|---|---|
| Example API/model concern | Exact target-version source | `path/to/file.py` | Confirmed / Unverified / N/A | Minimal change and regression test |

## Never state these without target-version evidence

- A core model, field, method, access mechanism, view syntax, RPC interface, or asset pipeline was removed or replaced.
- A specific Python or PostgreSQL version is required.
- A particular number of breaking changes exists.
- A migration script or API is officially supported for this exact transition.

The list above is a guardrail, not a claim that such changes did or did not happen. See [source-of-truth.md](source-of-truth.md) for trusted starting points.
