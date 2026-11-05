# Migration inventory: one addon per work unit

Copy this table into the task report or a project migration file. Do not mark an addon complete until the target-version checks were actually run.

## Project and database facts

| Item | Value | Evidence / confidence |
|---|---|---|
| Source Odoo version/commit |  |  |
| Target Odoo version/commit |  |  |
| Edition and hosting |  |  |
| Scope: code / database / both |  |  |
| Official DB upgrade path and intermediate hops |  |  |
| Test database and backup/restore verified |  |  |
| Python/PostgreSQL/runtime requirements |  |  |

## Addon inventory

| Technical addon | Provenance (first-party / third-party / unknown) | Source repo/maintainer | Dependencies | Target release found? | User choice (upstream / local port) | Status |
|---|---|---|---|---|---|---|
|  |  |  |  |  |  | not started |

## Per-addon evidence and checks

| Finding / syntax/API/data issue | Official evidence (URL, branch, path, commit) | File/line | Status (confirmed / N/A / unverified) | Minimal action | Test/check and result |
|---|---|---|---|---|---|
|  |  |  |  |  |  |

## Status meanings

- `not started`: inventory only or not yet examined.
- `researching`: version-specific evidence and compatibility being checked.
- `ported`: code edits made, but verification incomplete.
- `tests passed`: named target-version checks actually passed; list exactly what they prove.
- `blocked`: a known missing dependency, runtime, license/access, or unsupported route prevents progress.
- `unverified`: evidence or runtime is insufficient; not safe to treat as complete.

Track addon code status separately from database upgrade status. A green addon test does not establish database upgrade success.
