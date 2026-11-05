---
description: Plan or perform an evidence-based Odoo module migration between versions without guessing breaking changes.
argument-hint: [source version -> target version; module path]
---

Use the `odoo-migration` skill. Establish source and target versions, edition, and scope from $ARGUMENTS and the repository. Inspect the relevant module and official Odoo documentation/source for both versions. Produce a concise evidence table before edits. Apply only confirmed, module-relevant changes; mark unresolved findings unverified. Distinguish addon code porting from database upgrade and test execution. Never use an unsupported third-party breaking-change list as authority.
