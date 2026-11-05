---
name: odoo-feature-planning
description: Clarify and design non-trivial Odoo features or refactors before editing code, with concise requirements, architecture, and test plans.
---

# Odoo feature planning

Use for new features, broad refactors, or tasks with unresolved business rules. For a small, unambiguous change, keep planning brief and proceed; do not force a lengthy interview.

## Steps

1. Inspect the repository and relevant addon first: Odoo version/edition, module conventions, models, views, security, integrations, tests, and existing behavior.
2. State the problem and observable acceptance criteria in user terms. Ask focused questions only for decisions that materially affect behavior, data, security, or compatibility. Otherwise name conservative assumptions.
3. Explore one or two viable designs when there is a real tradeoff. Consider ORM ownership, access control, multi-company, data compatibility, user experience, and upgrade implications.
4. Recommend the smallest design that meets the criteria. Avoid speculative generalization, unnecessary dependencies, and unrelated cleanup.
5. Write an implementation sequence with affected files/components and a validation plan. Include test cases, install/update checks, and any migration/rollout risks.
6. For consequential architecture or data changes, present the plan for user agreement before editing. For straightforward contained work, state the plan and execute.
7. After implementation, compare results against each acceptance criterion and report checks actually run.

Planning is a communication aid, not a requirement to stop for approval on every low-risk coding task.
