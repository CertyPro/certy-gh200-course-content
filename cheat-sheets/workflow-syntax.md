# Cheat Sheet - Workflow Syntax

A quick reference to the core workflow keys. Workflows are YAML files in
`.github/workflows/`.

## Top-level skeleton

```yaml
name: CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Hello"
```

## `on:` - triggers

```yaml
on:
  push:
    branches: [main]
    paths: ["src/**"]
  pull_request:
    branches: [main]
  workflow_dispatch:
    inputs:
      environment:
        description: "Target environment"
        required: true
        default: "staging"
  schedule:
    - cron: "0 2 * * *"   # 02:00 UTC daily
  workflow_call:           # makes this a reusable workflow
```

Common events: `push`, `pull_request`, `workflow_dispatch` (manual),
`schedule` (cron), `workflow_call` (reusable), `repository_dispatch`,
`release`, `issues`. Filters: `branches`, `branches-ignore`, `paths`,
`paths-ignore`, `tags`, `tags-ignore`.

## `jobs:`

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps: [ ... ]
  test:
    needs: build          # runs after build succeeds
    runs-on: ubuntu-latest
    steps: [ ... ]
```

Jobs run in parallel by default. `needs` orders them and gates on success.

## `runs-on:` - choosing a runner

```yaml
runs-on: ubuntu-latest                 # GitHub-hosted
runs-on: [self-hosted, linux, x64]     # self-hosted by labels
```

## `steps:`

```yaml
steps:
  - name: Check out
    uses: actions/checkout@v4           # an action

  - name: Build
    run: npm run build                  # a shell command
    working-directory: ./app
```

A step is either `uses` (an action) or `run` (a shell command), not both.

## `needs` and job outputs

```yaml
jobs:
  setup:
    runs-on: ubuntu-latest
    outputs:
      version: ${{ steps.v.outputs.value }}
    steps:
      - id: v
        run: echo "value=1.2.3" >> "$GITHUB_OUTPUT"
  use:
    needs: setup
    runs-on: ubuntu-latest
    steps:
      - run: echo "${{ needs.setup.outputs.version }}"
```

## `if:` - conditions

```yaml
steps:
  - run: ./deploy.sh
    if: github.ref == 'refs/heads/main' && success()
```

Status functions: `success()`, `failure()`, `always()`, `cancelled()`.

## `env` - variables

```yaml
env:                       # workflow scope
  NODE_ENV: production
jobs:
  build:
    env:                   # job scope
      LOG_LEVEL: info
    steps:
      - run: echo "$NODE_ENV"
        env:               # step scope
          EXTRA: "1"
```

## `defaults`

```yaml
defaults:
  run:
    shell: bash
    working-directory: ./app
```

## `strategy.matrix`

```yaml
strategy:
  fail-fast: false
  max-parallel: 3
  matrix:
    os: [ubuntu-latest, windows-latest]
    node: [18, 20]
    include:
      - os: ubuntu-latest
        node: 22
    exclude:
      - os: windows-latest
        node: 18
runs-on: ${{ matrix.os }}
```

## `concurrency`

```yaml
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true
```

## `permissions`

```yaml
permissions:
  contents: read
  pull-requests: write
```

See the [security cheat sheet](security.md) for least-privilege guidance.
