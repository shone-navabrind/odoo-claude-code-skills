# Odoo task workflow: from request to verified change

This workflow adapts broadly useful practices from modular coding-agent skill systems (including the public Superpowers project) without copying its skill text or claiming hard technical enforcement. Follow the relevant stages in proportion to task size.

## 1. Discover and read relevant guidance

- Select the relevant plugin skills (module development; ORM; views; security; data/assets; install/update; testing; debugging; migration; review; verification).
- Read the relevant full skill instructions and inspect the project before relying on generic knowledge.
- Use specialist research only for facts that are version-dependent or not established by the repository. Prefer targeted primary-source lookups to broad, repeated searches.

## 2. Understand before changing

- Establish target behavior, acceptance criteria, risk, actual Odoo version/edition, module dependencies, and environment.
- Search narrowly; follow calls/inheritance/dependencies that matter. Keep unrelated code untouched.
- Ask only for essential missing requirements; state low-risk assumptions.

## 3. Plan proportionally

- For a small localized fix, use a short checklist and proceed.
- For a non-trivial feature/refactor, record design, affected files, dependency/security/data implications, and a test plan before implementation.
- For high-impact architecture or data changes, confirm the proposed direction before applying it.
- Prefer the smallest design that satisfies acceptance criteria; avoid speculative abstraction.

## 4. Implement and test

- For behavior changes, prefer a focused test-first loop when a relevant test and runnable environment exist: reproduce/fail, implement minimally, pass, then refactor.
- If red/green cannot be run, explain why; don't invent a test or claim a test-first cycle.
- Add coverage for access denial, multi-company, multi-record, repeatability, or data preservation where relevant.

## 5. Debug by evidence

- Reproduce and inspect the complete traceback/log context. Follow the earliest meaningful addon-owned frame and verify framework behavior for the exact version.
- Form hypotheses and test them with the smallest safe diagnostic. Do not layer guesses or hide errors by widening access, adding broad `sudo()`, or swallowing exceptions.
- After repeated failed fixes, stop and reconsider the model/configuration/data assumptions.

## 6. Verify before completion

- Inspect the final diff and run the checks relevant to the claim.
- Distinguish static checks, unit tests, module install/update, and full database upgrade—they prove different things.
- Report exact checks and results, blockers, assumptions, and residual risks. Never report a check as passed if it was not run.

## Safety boundary

Use development/test databases by default. Production install/update, migration, data repair, destructive operations, or deployment require explicit scope/authorization, verified backup/restore strategy, and a tested plan. Never include secret values in logs or answers.
