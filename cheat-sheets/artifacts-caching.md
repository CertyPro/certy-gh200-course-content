# Cheat Sheet - Artifacts and Caching

Two different features that learners often mix up.

- **Artifacts** share files between jobs in the same run and let you download
  outputs after a run finishes.
- **Caching** speeds up future runs by reusing files (usually dependencies)
  across runs.

## Artifacts

### Upload

```yaml
- uses: actions/upload-artifact@v4
  with:
    name: build-output
    path: dist/
    retention-days: 7      # optional override of the default retention
```

### Download

```yaml
- uses: actions/download-artifact@v4
  with:
    name: build-output
    path: dist/
```

Notes:

- Artifacts are scoped to a single workflow run. Use them to pass files from one
  job to a later job (with `needs`), or to keep build output for inspection.
- Retention has a default at repo or org level and can be overridden per upload.
- With `actions/upload-artifact@v4`, each artifact name within a run must be
  unique.

## Caching

```yaml
- uses: actions/cache@v4
  with:
    path: ~/.npm
    key: ${{ runner.os }}-npm-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-npm-
```

### How the key works

- **`key`** is the exact cache to look for. On a hit, the cache is restored and
  the step does not save a new one at the end.
- On a **miss**, the job runs, and at the end the cache is saved under `key`.
- **`restore-keys`** are ordered fallbacks. If the exact `key` is not found,
  GitHub tries each prefix in turn and restores the most recent match (a partial
  hit).
- Using `hashFiles('**/lock')` in the key means the cache rotates automatically
  when dependencies change.

### Common patterns

- Cache the package manager's download directory, not `node_modules`, where the
  ecosystem recommends it.
- Many setup actions (for example `actions/setup-node` with `cache: npm`) wrap
  caching for you.

## Artifacts vs cache - choose correctly

| Need | Use |
| --- | --- |
| Pass build output to a later job in the same run | Artifact |
| Keep test results or binaries to download after the run | Artifact |
| Reuse downloaded dependencies across runs to save time | Cache |

Caches are best-effort and may be evicted; never rely on a cache being present.
Artifacts are reliable within their retention window.
