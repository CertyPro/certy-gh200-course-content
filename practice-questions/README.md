# Practice Questions

Use these to check your understanding. They cover all five GH-200 domains.

## Full mock exam

The complete, weighted mock exam lives at **[certy.pro](https://certy.pro)**:

- 25 questions
- 70% to pass
- Weighted like the real GH-200 (domains 1.0 to 5.0 at 25 / 20 / 15 / 27 / 13 per
  cent)

Take it when you can answer the samples below without notes.

---

## Sample questions

### Q1 (Domain 1.0)
Which trigger lets a user start a workflow manually from the Actions tab, with
optional inputs?

- A. `schedule`
- B. `push`
- C. `workflow_dispatch`
- D. `repository_dispatch`

### Q2 (Domain 1.0)
You want job `test` to run only after job `build` succeeds and to read a value
`build` produced. Which two features do you need?

- A. `concurrency` and `env`
- B. `needs` and job `outputs`
- C. `if` and `secrets`
- D. `strategy` and `matrix`

### Q3 (Domain 2.0)
A job shows as "skipped" in the run summary. What is the most likely cause?

- A. The runner ran out of disk space
- B. An `if` condition was false or a `needs` dependency did not succeed
- C. A secret was missing
- D. The YAML failed to parse

### Q4 (Domain 2.0)
You need verbose internal logging from the runner to diagnose a tricky failure.
What should you set?

- A. `ACTIONS_RUNNER_DEBUG` to `true`
- B. `DEBUG` to `1`
- C. `VERBOSE` to `true`
- D. `LOG_LEVEL` to `debug` in `env`

### Q5 (Domain 3.0)
Which action type runs directly on the runner using the Actions toolkit and works
across Linux, Windows and macOS?

- A. Docker (container) action
- B. Composite action
- C. JavaScript action
- D. Reusable workflow

### Q6 (Domain 4.0)
At which scope do you configure a **required workflow** that must run across many
repositories?

- A. In each repository's settings
- B. At the organisation level
- C. In the workflow YAML with `on: required`
- D. In a runner group

### Q7 (Domain 5.0)
What is the recommended way to reference a third-party action so a moved tag
cannot inject malicious code?

- A. Pin to the `@main` branch
- B. Pin to a major version tag like `@v3`
- C. Pin to a full-length commit SHA
- D. Use `@latest`

### Q8 (Domain 5.0)
Your workflow deploys to AWS. How can you avoid storing long-lived cloud
credentials as secrets?

- A. Base64-encode the keys
- B. Use OIDC to request short-lived credentials with `id-token: write`
- C. Store them in `env` instead of `secrets`
- D. Print them to the log so they are masked

---

## Answers

| Q | Answer | Why |
| --- | --- | --- |
| 1 | **C** | `workflow_dispatch` adds a manual "Run workflow" button and supports `inputs`. `schedule`/`push` are automatic; `repository_dispatch` is triggered by an API call. |
| 2 | **B** | `needs` orders `test` after `build` and gates on its success; job `outputs` carry the value across, read via `needs.build.outputs.*`. |
| 3 | **B** | "Skipped" means the job did not meet its run conditions - a false `if` or an unmet `needs`. A parse error would fail the whole workflow, not skip a job. |
| 4 | **A** | `ACTIONS_RUNNER_DEBUG` enables runner diagnostic logging; `ACTIONS_STEP_DEBUG` enables step debug logging. The others are not recognised by Actions. |
| 5 | **C** | JavaScript actions run on the runner via Node and are cross-platform. Docker actions are Linux-only; composite actions bundle steps; a reusable workflow is not an action type. |
| 6 | **B** | Required workflows are configured at the organisation level and applied to selected repositories. |
| 7 | **C** | A commit SHA is immutable, so a compromised or moved tag cannot change the code you run. Keep SHAs current with Dependabot. |
| 8 | **B** | OIDC lets the workflow exchange a signed token for short-lived cloud credentials, removing the need for stored static keys. It requires `permissions: id-token: write`. |

Score yourself, revisit the weakest domain, then take the full mock exam at
[certy.pro](https://certy.pro).
