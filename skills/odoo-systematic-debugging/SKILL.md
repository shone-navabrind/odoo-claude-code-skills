---
name: odoo-systematic-debugging
description: Diagnose Odoo exceptions, failed installs/upgrades, incorrect behavior, and performance symptoms systematically before changing code.
---

# Systematic Odoo debugging

Use this skill when a user reports an error, regression, failed install/update, incorrect output, or unexplained slowdown. The goal is to identify the first project-owned root cause, not to patch the last visible symptom.

## 1. Establish the failure precisely

- Capture the complete traceback/log context, exact command or UI action, expected vs actual behavior, reproducibility, and whether this is dev/test/staging/production.
- Detect Odoo version/commit, edition, installed modules, Python/runtime environment, and relevant configuration. Do not print secrets or request credentials.
- Check whether the failure occurs on a clean baseline, only after an update, only for one user/company, or only with particular data.
- Protect production: do not run update/install, destructive SQL, shell actions, or data repair on production without explicit authorization, backup, and an approved plan.

## 2. Trace evidence to root cause

- Start at the earliest meaningful traceback frame owned by the custom addon; read the surrounding method and callers, and then inspect the relevant framework call path/source if needed.
- For XML/view failures, identify the exact file, external ID, inherited view chain, XPath target, load order, and dependency providing referenced records.
- For registry/import failures, check Python imports, `__init__.py` chains, manifest dependencies, syntax, model names, and whether the target runtime sees the addon path.
- For access failures, identify the executing user, operation, model, ACLs, record rules, company context, and any `sudo()` boundary. Don't “fix” these by broadening permissions blindly.
- For data/install/update failures, distinguish schema/data state, module state, XML ID conflicts, dependency/load-order issues, and code incompatibility. Inspect logs before attempting recovery.
- For performance, reproduce with representative data and use profiling/query evidence; avoid speculative caching or SQL rewrites.

## 3. Use explicit hypotheses

Write a short list of plausible causes and the evidence that would confirm or reject each. Run the smallest safe, read-only or isolated diagnostic first. Change one causal factor at a time and preserve the original error for comparison.

After repeated unsuccessful fixes (roughly three), stop patching: summarize disproven hypotheses, re-check assumptions and call paths, and consider a design/configuration/data issue or ask for missing evidence.

## 4. Fix and verify

- Make the smallest root-cause change; add a focused regression test or reproducible check.
- Re-run the exact failing scenario plus the narrow relevant test suite in a disposable development/test environment.
- Distinguish a code fix from recovery of a database already left in a partially updated state; do not prescribe manual SQL without a backed-up, reviewed recovery plan.
- Report root cause, evidence, changes, exact verification performed, unverified risks, and safe next steps.

Never claim a diagnosis or fix is confirmed solely because an exception disappeared. Verify the intended behavior and relevant neighboring behavior.
