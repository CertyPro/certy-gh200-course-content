# Cheat Sheet - Reusable Workflows

A reusable workflow is a whole workflow that other workflows call, so you can
write logic once and use it across many repos. See real examples in
[gh200-reusable-workflows-library](https://github.com/CertyPro/gh200-reusable-workflows-library).

## Defining a reusable workflow

Mark it callable with `on: workflow_call` and declare its `inputs`, `secrets` and
`outputs`.

```yaml
# .github/workflows/deploy.yml (the reusable workflow)
name: Reusable deploy
on:
  workflow_call:
    inputs:
      environment:
        description: "Target environment"
        required: true
        type: string
    secrets:
      deploy_token:
        required: true
    outputs:
      url:
        description: "Deployed URL"
        value: ${{ jobs.deploy.outputs.url }}

jobs:
  deploy:
    runs-on: ubuntu-latest
    outputs:
      url: ${{ steps.do.outputs.url }}
    steps:
      - id: do
        run: echo "url=https://example.com" >> "$GITHUB_OUTPUT"
        env:
          TOKEN: ${{ secrets.deploy_token }}
```

Input `type` can be `string`, `number` or `boolean`.

## Calling a reusable workflow

Call it as a **job**, using `uses:` at the job level (not inside `steps`).

```yaml
# .github/workflows/ci.yml (the caller)
name: CI
on: [push]

jobs:
  call-deploy:
    uses: octo-org/repo/.github/workflows/deploy.yml@v1
    with:
      environment: staging
    secrets:
      deploy_token: ${{ secrets.DEPLOY_TOKEN }}
```

### Referencing

- Same repo: `uses: ./.github/workflows/deploy.yml`.
- Another repo: `uses: owner/repo/.github/workflows/deploy.yml@<ref>` where the
  ref is a tag, branch or SHA.

### Passing secrets

- Pass secrets explicitly under `secrets:`, or use `secrets: inherit` to forward
  all of the caller's secrets.

```yaml
jobs:
  call:
    uses: owner/repo/.github/workflows/deploy.yml@v1
    secrets: inherit
```

## Reusable workflows vs composite actions

| | Reusable workflow | Composite action |
| --- | --- | --- |
| Granularity | A whole workflow (jobs) | A set of steps within one job |
| Called with | `uses:` at the **job** level | `uses:` at the **step** level |
| Can define jobs | Yes | No (steps only) |
| Good for | Standard pipelines shared across repos | Reusable step sequences |

## Exam tips

- A reusable workflow is invoked at the **job** level; a composite action at the
  **step** level.
- Declare `inputs`, `secrets` and `outputs` under `workflow_call`.
- Outputs of a reusable workflow come from its jobs' outputs.
- Sharing reusable workflows across an organisation is a key enterprise
  capability (domain 4.0).
