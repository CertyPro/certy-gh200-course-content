# Glossary

Key GH-200 terms in plain English.

**Workflow** - an automated process defined in a YAML file in
`.github/workflows/`. It is triggered by events and contains one or more jobs.

**Job** - a set of steps that run on a single runner. Jobs run in parallel by
default, or in order when linked with `needs`.

**Step** - a single task in a job. A step is either a shell command (`run`) or a
call to an action (`uses`).

**Action** - a reusable unit of code packaged to be used in a step. Comes in three
types: composite, JavaScript and Docker (container).

**Runner** - the machine that executes a job. Either GitHub-hosted or self-hosted,
chosen with `runs-on`.

**Self-hosted runner** - a runner you provide and manage yourself, useful for
custom hardware, private networks or special tools. You own its security and
upkeep.

**Runner group** - an access-control grouping that decides which repositories and
workflows may use a set of runners. Not the same as a runner label.

**Matrix** - a `strategy.matrix` that runs a job many times across combinations of
values (for example several OS and language versions).

**Artifact** - files produced by a run and shared between jobs in that run or
downloaded afterwards. Scoped to a single run and kept for a retention period.

**Cache** - files (usually dependencies) saved and restored across runs to save
time, via `actions/cache`. Best-effort and keyed; may be evicted.

**Reusable workflow** - a whole workflow that other workflows call with `uses:` at
the job level. Defined with `on: workflow_call` and its `inputs`, `secrets` and
`outputs`.

**Composite action** - an action that bundles several steps into one, called with
`uses:` at the step level. Pure YAML plus shell, no separate jobs.

**JavaScript action** - an action that runs directly on the runner using Node and
the Actions toolkit. Cross-platform and fast.

**Docker (container) action** - an action that runs inside a container from a
Dockerfile or image. Most control over the environment but Linux runners only.

**`GITHUB_TOKEN`** - an automatic, short-lived token created for each run so a
workflow can interact with the repository. Scope it with `permissions`.

**Secret** - an encrypted value (such as an API key) stored at repo, environment
or organisation level. Masked in logs and never written into the YAML.

**Environment** - a named deployment target with protection rules such as required
reviewers, wait timers, deployment branch rules and scoped secrets.

**OIDC** - OpenID Connect. Lets a workflow exchange a signed token for short-lived
cloud credentials, removing the need to store long-lived keys.

**Concurrency** - controls overlapping runs. A `concurrency` group with
`cancel-in-progress` stops superseded runs.

**`needs`** - declares that a job depends on others; it runs after them and only
if they succeeded, and can read their outputs.

**Context** - a collection of run data you read in expressions, such as `github`,
`env`, `secrets`, `matrix`, `needs`, `inputs` and `vars`.

**Expression** - logic written `${{ ... }}` that reads contexts and calls
functions to compute values and conditions.

**Required workflow** - a workflow configured at the organisation level that must
run across selected repositories.

**Dependabot** - GitHub's tool that opens pull requests to update dependencies,
including your pinned actions when set to the `github-actions` ecosystem.
