# GH-200 Exam Objectives

This is the objective map for the GitHub Actions certification (**GH-200**). It
lists the five exam domains, their official weights, the skills each one tests,
the matching Certy lesson and the practice repo to use.

| Domain | Title | Weight |
| --- | --- | --- |
| 1.0 | Author and manage workflows | 25% |
| 2.0 | Consume and troubleshoot workflows | 20% |
| 3.0 | Author and maintain actions | 15% |
| 4.0 | Manage GitHub Actions for the enterprise | 27% |
| 5.0 | Secure and optimise automation | 13% |

Treat the weights as a study budget. Domain 4.0 (enterprise) is the largest, with
domain 1.0 close behind, so spend most of your revision there.

---

## Domain 1.0 - Author and manage workflows (25%)

**Certy lesson:** first-workflow
**Practice repos:** [gh200-student-actions-lab](https://github.com/CertyPro/gh200-student-actions-lab),
[gh200-reusable-workflows-library](https://github.com/CertyPro/gh200-reusable-workflows-library)

You should be able to:

- Create a workflow file in `.github/workflows/` and understand that workflows are
  YAML.
- Trigger workflows with events using `on:` - for example `push`, `pull_request`,
  `workflow_dispatch` (manual, with inputs), `schedule` (cron) and
  `repository_dispatch`.
- Configure event filters such as `branches`, `branches-ignore`, `paths`,
  `paths-ignore` and `tags`.
- Define `jobs`, the steps within them, and choose runners with `runs-on`.
- Order jobs with `needs` and pass data between them with job `outputs`.
- Use `run` steps (shell commands) and `uses` steps (calling actions).
- Set environment variables at workflow, job and step level with `env`, and use
  `defaults` (for example `defaults.run.shell` and `working-directory`).
- Run steps conditionally with `if` and status check functions such as
  `success()`, `failure()`, `always()` and `cancelled()`.
- Build a build matrix with `strategy.matrix`, including `include`, `exclude`,
  `fail-fast` and `max-parallel`.
- Add manual approval and protection with `environments`.
- Control concurrent runs with `concurrency` and `cancel-in-progress`.
- Author and call reusable workflows with `workflow_call`.

---

## Domain 2.0 - Consume and troubleshoot workflows (20%)

**Certy lesson:** consuming-workflows
**Practice repo:** [gh200-broken-workflows](https://github.com/CertyPro/gh200-broken-workflows)

You should be able to:

- Find and read run logs in the Actions tab, expand step output and locate the
  failing step.
- Re-run all jobs, re-run only failed jobs, and re-run with debug logging.
- Enable step debug logging (`ACTIONS_STEP_DEBUG`) and runner diagnostic logging
  (`ACTIONS_RUNNER_DEBUG`) using secrets or variables.
- Interpret common failures: bad YAML, wrong event, skipped jobs, failed status
  checks, missing permissions, missing secrets and expired or wrong runner labels.
- Use workflow commands in logs such as `::error::`, `::warning::`, `::notice::`
  and `::group::` / `::endgroup::`.
- Consume artifacts and caches produced by other jobs and understand why a cache
  miss happened.
- Search, filter and disable or enable workflows from the UI and the API.
- Read workflow run status from commits, pull requests and the Checks API.
- Use the GitHub CLI (`gh run list`, `gh run view`, `gh run rerun`) to inspect
  runs.

---

## Domain 3.0 - Author and maintain actions (15%)

**Certy lesson:** building-actions
**Practice repo:** [gh200-custom-actions-lab](https://github.com/CertyPro/gh200-custom-actions-lab)

You should be able to:

- Explain the three action types: composite, JavaScript and Docker (container)
  actions, and choose the right one for a task.
- Write an `action.yml` metadata file defining `name`, `description`, `inputs`,
  `outputs` and `runs`.
- Build a composite action that bundles several steps with `runs.using:
  "composite"`.
- Build a JavaScript action with `runs.using: "node20"` and the
  `@actions/core` / `@actions/github` toolkit.
- Build a Docker container action with `runs.using: "docker"` and a Dockerfile or
  pre-built image.
- Read inputs (`with:` / `INPUT_*`) and set outputs through the
  `$GITHUB_OUTPUT` file.
- Version and publish an action: tags, semantic version branches (for example
  moving `v1`), and the GitHub Marketplace.
- Maintain an action: changelogs, releases and keeping dependencies current.

---

## Domain 4.0 - Manage GitHub Actions for the enterprise (27%)

**Certy lesson:** governance-and-scale
**Practice repos:** [gh200-enterprise-admin-sim](https://github.com/CertyPro/gh200-enterprise-admin-sim),
[gh200-reusable-workflows-library](https://github.com/CertyPro/gh200-reusable-workflows-library)

You should be able to:

- Enable or disable Actions and set allowed actions policies at the repository,
  organisation and enterprise levels (allow all, local only, or an allow list).
- Require actions to be pinned and allow specific actions or publishers.
- Manage self-hosted runners and **runner groups**, and control which
  repositories and workflows can use each group.
- Configure GitHub-hosted larger runners and manage who can use them.
- Manage usage, billing and spending limits for Actions minutes and storage.
- Configure **required workflows** so selected workflows run across an
  organisation's repositories.
- Manage organisation and repository **secrets and variables**, including scoping
  secrets to selected repositories.
- Set artifact and log **retention** policies.
- Share actions and reusable workflows internally across an organisation.
- Use the API and audit log to monitor and govern Actions usage.

---

## Domain 5.0 - Secure and optimise automation (13%)

**Certy lesson:** securing-actions
**Practice repos:** [gh200-security-challenges](https://github.com/CertyPro/gh200-security-challenges),
[gh200-student-actions-lab](https://github.com/CertyPro/gh200-student-actions-lab)

You should be able to:

- Apply least privilege to the automatic `GITHUB_TOKEN` with the `permissions`
  key at workflow and job level.
- Store and use **secrets** safely, understand masking, and know secrets are not
  passed to workflows triggered by forks via `pull_request`.
- Pin third-party actions to a full-length commit **SHA** rather than a tag.
- Use **environments** with required reviewers, wait timers and deployment branch
  rules to protect deployments.
- Configure **OIDC** so workflows request short-lived cloud credentials instead of
  storing long-lived secrets.
- Understand the risk of `pull_request_target` and untrusted input, and avoid
  script injection in `run` steps.
- Keep actions current with **Dependabot** version updates.
- Optimise cost and speed with caching, artifact retention, matrix tuning,
  concurrency and choosing the right runner size.

---

## Quick mapping

| Domain | Weight | Certy lesson | Primary practice repo |
| --- | --- | --- | --- |
| 1.0 | 25% | first-workflow | gh200-student-actions-lab |
| 2.0 | 20% | consuming-workflows | gh200-broken-workflows |
| 3.0 | 15% | building-actions | gh200-custom-actions-lab |
| 4.0 | 27% | governance-and-scale | gh200-enterprise-admin-sim |
| 5.0 | 13% | securing-actions | gh200-security-challenges |

Take the full weighted mock exam at [certy.pro](https://certy.pro) when you can
answer the "you should be able to" lists without notes.
