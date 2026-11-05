# Odoo error triage quick reference

Use the complete [systematic debugging skill](../skills/odoo-systematic-debugging/SKILL.md) for a reported failure. This page is a compact triage map, not a claim that every symptom has a single cause.

| Symptom | First evidence to inspect | Common investigation directions |
|---|---|---|
| Addon not visible/not found | Active process config, effective addons paths, technical directory name, manifest | Wrong config/container mount, missing path, module list refresh/cache behavior; verify for the installed version |
| Import or registry traceback | Full traceback, earliest addon-owned frame, import chain | Syntax/import error, missing `__init__.py` import, missing dependency, incompatible override |
| XML parse/view validation error | First failing file/record/line, module load order, inherited view chain | Malformed XML, unavailable external ID, missing dependency, invalid XPath or version-specific view syntax |
| Access denied / record missing for user | User, operation/model, ACL, rules, active company/context | Missing intended grant, intersecting domains/context, rule logic; UI visibility is not authorization |
| Install/update failure | Exact command, exit status, first complete server error, current DB/environment | Wrong database, missing dependency, stale process/source path, schema/data state, partial update; don't repeatedly retry valuable DB |
| Field/method missing | Model registry, module dependencies, imports, source version | Module not loaded, wrong dependency/order, typo, stale process, version mismatch |
| Slow request | Repro steps and representative dataset, logs/profiler/query evidence | N+1 access, unbounded searches, repeated computes, inefficient domains; measure before optimization |
| Browser-only failure | Browser console/network plus server logs and loaded assets | Asset declaration/build/cache, JS exception, RPC response; test using target version's asset conventions |

## Safe sequence

1. Preserve full logs and note the exact action and environment; redact secrets.
2. Reproduce in development/test if possible.
3. Follow traceback frames into project code and inspect callers/configuration.
4. Form/test hypotheses one at a time, beginning with read-only checks.
5. Fix root cause, add regression coverage, then verify the actual intended behavior.
6. For a partially failed module update, stop before retrying on valuable data; recover or continue only from a clone/backup with a reviewed plan.
