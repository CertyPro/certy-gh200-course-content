# Module 04 - Manage GitHub Actions for the enterprise

**Domain 4.0 (27%) | Certy lesson: governance-and-scale**
**Practice repos:** [gh200-enterprise-admin-sim](https://github.com/CertyPro/gh200-enterprise-admin-sim),
[gh200-reusable-workflows-library](https://github.com/CertyPro/gh200-reusable-workflows-library)

This is the heaviest module on the exam. It is about administering Actions at
scale - policy, runners, secrets, billing and governance across many repos. The
admin sim repo reproduces the relevant settings screens and exercises.

## Concepts to teach

- **Policy levels:** Actions can be enabled or disabled, and allowed actions set,
  at **repository**, **organisation** and **enterprise** levels. The hierarchy
  flows down - a higher level can constrain a lower one.
- **Allowed actions policies:** allow all actions, allow only actions in the same
  repository or organisation (local only), or allow a specific list (plus the
  option to allow GitHub-created and verified-creator actions).
- **Self-hosted runners and runner groups:** register runners, organise them into
  **runner groups**, and control which repositories and workflows may use each
  group.
- **Larger GitHub-hosted runners:** more cores and memory, managed at org level,
  with access controls.
- **Required workflows:** define workflows that must run across selected
  repositories in an organisation.
- **Secrets and variables at scale:** organisation-level secrets and variables,
  scoped to all, private or selected repositories.
- **Retention:** artifact and log retention policies.
- **Sharing internally:** sharing actions and reusable workflows across an
  organisation (the reusable workflows library shows this in practice).
- **Billing and limits:** Actions minutes and storage, spending limits, and usage
  reports.
- **Governance:** the audit log and the API for monitoring Actions activity.

## Common mistakes

- Confusing the three policy levels, or assuming a repo can override a stricter
  org or enterprise policy.
- Mixing up **runner groups** (access control over runners) with runner
  **labels** (how a job selects a runner).
- Setting a secret at repo level when it should be an org secret scoped to
  selected repos.
- Forgetting that required workflows are configured at the organisation, not in
  each repo.
- Overlooking storage costs from long artifact retention.

## What to demo live

1. In gh200-enterprise-admin-sim, walk through the allowed actions policy at repo
   then org level and show how the org setting constrains the repo.
2. Create a runner group and restrict it to selected repositories.
3. Add an organisation secret scoped to selected repositories.
4. Configure a required workflow across the org's repos.
5. Show artifact retention settings and the usage and billing view.
6. In gh200-reusable-workflows-library, show how a shared reusable workflow is
   consumed from another repo.

Pair this with the [reusable workflows](../../cheat-sheets/reusable-workflows.md),
[runners](../../cheat-sheets/runners.md) and
[security](../../cheat-sheets/security.md) cheat sheets.
