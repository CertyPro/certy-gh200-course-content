# Cheat Sheet - Contexts and Expressions

Expressions let you read data and make decisions inside a workflow. They are
written `${{ ... }}`.

## Expression syntax

```yaml
if: ${{ github.event_name == 'push' }}
run: echo "Branch is ${{ github.ref_name }}"
```

In an `if:` you may omit the `${{ }}`:

```yaml
if: github.ref == 'refs/heads/main'
```

Operators: `==`, `!=`, `<`, `<=`, `>`, `>=`, `&&`, `||`, `!`.

## Common contexts

### `github`
Information about the run and the event.

| Field | Meaning |
| --- | --- |
| `github.repository` | `owner/repo` |
| `github.ref` | full ref, e.g. `refs/heads/main` |
| `github.ref_name` | short ref, e.g. `main` |
| `github.sha` | commit SHA |
| `github.event_name` | event that triggered the run |
| `github.actor` | user that triggered the run |
| `github.run_id` / `github.run_number` | run identifiers |
| `github.event` | the full event payload |
| `github.token` | the automatic `GITHUB_TOKEN` |

### `env`
Variables defined with `env:`.

```yaml
run: echo "${{ env.NODE_ENV }}"
```

### `secrets`
Secrets configured for the repo, environment or organisation.

```yaml
with:
  token: ${{ secrets.MY_TOKEN }}
```

`secrets.GITHUB_TOKEN` is the automatic token. Secrets are masked in logs and are
not passed to fork-triggered `pull_request` runs.

### `matrix`
The current matrix combination.

```yaml
runs-on: ${{ matrix.os }}
run: echo "Node ${{ matrix.node }}"
```

### `needs`
Outputs and results of jobs this job depends on.

```yaml
run: echo "${{ needs.build.outputs.version }}"
if: ${{ needs.build.result == 'success' }}
```

### Other contexts
`vars` (configuration variables), `inputs` (workflow_dispatch and workflow_call
inputs), `job`, `steps`, `runner`, `strategy`.

## Functions

| Function | Use |
| --- | --- |
| `contains(a, b)` | true if `a` contains `b` |
| `startsWith(s, p)` / `endsWith(s, p)` | string prefix / suffix tests |
| `format('{0}-{1}', a, b)` | string formatting |
| `join(array, sep)` | join an array into a string |
| `toJSON(value)` / `fromJSON(string)` | convert to / from JSON |
| `hashFiles('**/lock')` | hash of matched files (great for cache keys) |

## Status check functions

Use these in `if:` to react to earlier results.

| Function | Runs the step when |
| --- | --- |
| `success()` | all previous steps succeeded (default behaviour) |
| `failure()` | a previous step failed |
| `always()` | always, even if cancelled or failed |
| `cancelled()` | the run was cancelled |

```yaml
- name: Upload logs on failure
  if: ${{ failure() }}
  uses: actions/upload-artifact@v4
  with:
    name: logs
    path: ./logs
```

## Passing data between steps

```yaml
- run: echo "result=ok" >> "$GITHUB_OUTPUT"   # step output
  id: step1
- run: echo "MY_VAR=value" >> "$GITHUB_ENV"   # env var for later steps
- run: echo "${{ steps.step1.outputs.result }}"
```
