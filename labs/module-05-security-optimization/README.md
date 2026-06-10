# Module 05 - Secure and optimise automation

**Domain 5.0 (13%) | Certy lesson: securing-actions**
**Practice repos:** [gh200-security-challenges](https://github.com/CertyPro/gh200-security-challenges),
[gh200-student-actions-lab](https://github.com/CertyPro/gh200-student-actions-lab)

The smallest module by weight but a frequent source of real-world incidents.
Teach both halves: keep automation secure, and keep it fast and cheap.

## Concepts to teach

### Security

- **Least privilege for `GITHUB_TOKEN`:** set `permissions` at workflow and job
  level. Default to `contents: read` and grant only what is needed.
- **Secrets:** how to store them, that GitHub masks them in logs, and that
  secrets are **not** available to workflows triggered by `pull_request` from a
  fork.
- **SHA pinning:** pin third-party actions to a full-length commit SHA, not a
  mutable tag, so a compromised tag cannot inject code.
- **Environments:** required reviewers, wait timers and deployment branch rules to
  gate deployments.
- **OIDC:** configure OpenID Connect so a workflow requests short-lived cloud
  credentials instead of storing long-lived secrets.
- **Untrusted input:** the danger of `pull_request_target`, and avoiding script
  injection by not interpolating untrusted values straight into `run` steps.
- **Dependabot:** automatic version updates for the actions you depend on.

### Optimisation

- **Caching** dependencies with `actions/cache` to cut install time.
- **Artifact and log retention** to control storage cost.
- **Matrix tuning** with `max-parallel` and sensible `exclude`.
- **Concurrency** to cancel superseded runs.
- **Right-sizing runners** so you do not pay for more than you need.

## Common mistakes

- Leaving `GITHUB_TOKEN` at broad default permissions instead of narrowing them.
- Pinning to `@v3` and assuming that is secure - a tag can be moved; a SHA cannot.
- Echoing a secret into a log expecting masking to hide a transformed value.
- Using `pull_request_target` with checkout of untrusted code, which can leak
  secrets.
- Building a cache key that never changes, so it goes stale, or one that always
  changes, so it never hits.
- Storing long-lived cloud keys as secrets when OIDC would remove them entirely.

## What to demo live

1. In gh200-security-challenges, tighten an over-privileged `GITHUB_TOKEN` with a
   minimal `permissions` block.
2. Replace a tag-pinned third-party action with a SHA pin.
3. Configure an environment with a required reviewer and show the deployment
   pausing for approval.
4. Walk through an OIDC trust setup conceptually and show the workflow requesting
   a token.
5. In gh200-student-actions-lab, add `actions/cache` and show the time saved on a
   second run, then add `concurrency` with `cancel-in-progress`.

Pair this with the [security](../../cheat-sheets/security.md) and
[artifacts and caching](../../cheat-sheets/artifacts-caching.md) cheat sheets.
