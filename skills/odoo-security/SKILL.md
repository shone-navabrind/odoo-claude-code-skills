---
name: odoo-security
 description: Add or review Odoo ACLs, groups, record rules, company isolation, and access checks.
---

# Odoo security

Treat security as server-side behavior, not presentation. Inspect the model, all entry points, existing groups/ACLs/rules, and target-version semantics before changing access.

## Checklist

- Define who may read, create, write, and delete each model; follow least privilege.
- Check `ir.model.access.csv` model references, group external IDs, and CSV load order. ACL grants combine; do not assume one restrictive row cancels another grant.
- Review record rules, global/group rule combination, domains, company context, and multi-company isolation using the target version's documented behavior.
- Verify public methods, controllers, RPC-exposed actions, wizards, and elevated `sudo()` paths cannot bypass intended checks.
- Do not secure data by hiding menus/buttons or setting fields readonly in views.
- Avoid broad `sudo()`; where elevation is required, constrain records and validate the caller's authority and inputs.
- Test allowed and denied access for representative groups and companies, including direct ORM/API access.
- Never weaken production access to make tests or installation pass without explaining the intended permission change.

Do not claim core security models or APIs changed in a version unless official target-version evidence supports it. See `../odoo-migration/SKILL.md` for migration evidence rules.
