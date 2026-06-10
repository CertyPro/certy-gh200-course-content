# Cheat Sheet - Security

Securing Actions is domain 5.0, and it overlaps with enterprise governance
(domain 4.0). Practise these in
[gh200-security-challenges](https://github.com/CertyPro/gh200-security-challenges).

## `GITHUB_TOKEN` permissions

Every run gets an automatic `GITHUB_TOKEN`. Apply least privilege with the
`permissions` key. Default to read-only and grant only what a job needs.

```yaml
permissions:
  contents: read          # workflow-wide default

jobs:
  release:
    permissions:
      contents: write     # this job needs to push a tag
      packages: write
    runs-on: ubuntu-latest
    steps: [ ... ]
```

- Setting any single scope sets all unspecified scopes to `none`.
- `permissions: {}` grants nothing.
- Job-level `permissions` override the workflow-level default for that job.

## Secrets

- Store secrets at repo, environment or organisation level - never in the YAML.
- GitHub masks secret values in logs, but transformed or partial values can still
  leak, so do not print them.
- Secrets are **not** passed to workflows triggered by `pull_request` from a fork.
- Organisation secrets can be scoped to all, private or selected repositories.

```yaml
steps:
  - run: ./deploy.sh
    env:
      TOKEN: ${{ secrets.DEPLOY_TOKEN }}
```

## Pin actions to a SHA

Tags can be moved; a commit SHA cannot. Pin third-party actions to a full-length
SHA to defend against a compromised tag.

```yaml
# Riskier - tag can be moved
- uses: some/action@v3

# Safer - immutable commit SHA
- uses: some/action@a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0
```

Keep pinned SHAs current with Dependabot (see below).

## Environments

Environments add gates to deployments.

- **Required reviewers** - a person must approve before the job runs.
- **Wait timer** - a delay before the job proceeds.
- **Deployment branch rules** - only listed branches may deploy.
- Environment-scoped secrets are only available to jobs targeting that
  environment.

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: production    # triggers the environment's protection rules
    steps: [ ... ]
```

## OIDC (OpenID Connect) - overview

OIDC lets a workflow request a short-lived token from a cloud provider instead of
storing long-lived secrets.

- The workflow needs `permissions: id-token: write`.
- GitHub issues a signed OIDC token describing the run.
- The cloud provider's trust policy verifies the claims (repo, branch,
  environment) and returns temporary credentials.
- Result: no static cloud keys stored as secrets.

```yaml
permissions:
  id-token: write
  contents: read
```

## Untrusted input

- `pull_request_target` runs with the base repo's secrets and write token; do not
  check out and run untrusted PR code under it.
- Avoid script injection: never interpolate untrusted values (issue titles, PR
  bodies) directly into a `run` command. Pass them through `env` and reference the
  variable instead.

```yaml
# Risky
- run: echo "${{ github.event.issue.title }}"
# Safer
- run: echo "$TITLE"
  env:
    TITLE: ${{ github.event.issue.title }}
```

## Dependabot

Enable Dependabot version updates for the `github-actions` ecosystem to get
pull requests that bump your pinned actions.

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
```

## Checklist

- [ ] `permissions` set to least privilege.
- [ ] No secrets hard-coded in YAML.
- [ ] Third-party actions pinned to a SHA.
- [ ] Deployments gated by environments.
- [ ] OIDC used instead of long-lived cloud keys where possible.
- [ ] No untrusted input interpolated into `run` steps.
- [ ] Dependabot updating actions.
