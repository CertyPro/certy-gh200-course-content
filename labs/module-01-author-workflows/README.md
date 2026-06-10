# Module 01 - Author and manage workflows

**Domain 1.0 (25%) | Certy lesson: first-workflow**
**Practice repos:** [gh200-student-actions-lab](https://github.com/CertyPro/gh200-student-actions-lab),
[gh200-reusable-workflows-library](https://github.com/CertyPro/gh200-reusable-workflows-library)

This is the foundation module and the second-heaviest on the exam. If learners are
comfortable here, the rest of the course builds cleanly on it.

## Concepts to teach

- **Where workflows live:** YAML files in `.github/workflows/`. A repo can have
  many workflow files.
- **The structure:** `name`, `on`, `jobs`. Each job has `runs-on` and a list of
  `steps`. Steps are either `run` (shell) or `uses` (an action).
- **Triggers (`on:`):** `push`, `pull_request`, `workflow_dispatch` (manual, with
  optional `inputs`), `schedule` (cron), and `workflow_call`. Show event filters:
  `branches`, `paths`, `tags`.
- **Runners (`runs-on`):** GitHub-hosted labels like `ubuntu-latest`, and how
  self-hosted runners are selected by labels.
- **Job dependencies:** `needs` to order jobs, and job `outputs` to pass data
  downstream.
- **Variables and defaults:** `env` at workflow, job and step scope; `defaults`
  for shell and working directory.
- **Conditionals:** `if:` with expressions and status functions (`success()`,
  `failure()`, `always()`).
- **Matrices:** `strategy.matrix` with `include`, `exclude`, `fail-fast`,
  `max-parallel`.
- **Concurrency:** `concurrency` groups and `cancel-in-progress`.
- **Reusable workflows:** authoring with `on: workflow_call` and calling with
  `uses:` (use the reusable workflows library for this).

## Common mistakes

- Wrong indentation in YAML - the single most common reason a workflow does not
  appear or fails to parse.
- Confusing `env` (variables) with `with` (action inputs) and `secrets`.
- Forgetting that `needs` both orders jobs and gates them on success.
- Expecting `workflow_dispatch` to appear before the workflow exists on the
  default branch.
- Treating each step as sharing process state - each `run` step is a fresh shell;
  use `$GITHUB_ENV` and `$GITHUB_OUTPUT` to pass values on.
- Using a matrix without `fail-fast: false` and then being surprised that one
  failure cancels the others.

## What to demo live

1. In gh200-student-actions-lab, create a minimal workflow on `push` that checks
   out the code and prints a message, and watch it run in the Actions tab.
2. Add a second job with `needs` and pass an output between jobs.
3. Add a `strategy.matrix` across a couple of versions and show parallel jobs.
4. Add `workflow_dispatch` with an input and trigger it manually.
5. Switch to gh200-reusable-workflows-library and call a reusable workflow with
   `uses:`, passing `inputs` and `secrets`.

Pair this with the [workflow syntax](../../cheat-sheets/workflow-syntax.md) and
[contexts and expressions](../../cheat-sheets/contexts-expressions.md) cheat
sheets.
