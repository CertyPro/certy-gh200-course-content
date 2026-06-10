# Module 02 - Consume and troubleshoot workflows

**Domain 2.0 (20%) | Certy lesson: consuming-workflows**
**Practice repo:** [gh200-broken-workflows](https://github.com/CertyPro/gh200-broken-workflows)

This module is about reading what GitHub tells you and fixing it. The broken
workflows repo is built for exactly this - every workflow fails in an instructive
way.

## Concepts to teach

- **Reading run logs:** the Actions tab, the run summary, expanding jobs and steps
  to find the failing line.
- **Re-running:** re-run all jobs, re-run only failed jobs, and re-run with debug
  logging enabled.
- **Debug logging:** set `ACTIONS_STEP_DEBUG` and `ACTIONS_RUNNER_DEBUG` (as
  secrets or variables) to get verbose output.
- **Workflow commands in logs:** `::error::`, `::warning::`, `::notice::`, and
  grouping with `::group::` / `::endgroup::`.
- **Status and checks:** how run status shows on commits and pull requests, and
  how branch protection uses required status checks.
- **Consuming outputs:** downloading artifacts and understanding cache hits and
  misses produced by other jobs.
- **The GitHub CLI:** `gh run list`, `gh run view --log`, `gh run rerun`,
  `gh run watch`.

## Common mistakes

- Reading only the red summary and never expanding the failing step.
- Assuming a "skipped" job failed - skipped usually means an `if` condition or a
  `needs` dependency was not met.
- Blaming the action when the real issue is a missing secret or insufficient
  `permissions`.
- Not realising secrets are not available to workflows from forked pull requests.
- Expecting a cache hit when the cache key changed (so it was a clean miss, not a
  bug).
- Forgetting that a workflow only runs for an event the file actually subscribes
  to in `on:`.

## What to demo live

1. Open a failing run in gh200-broken-workflows and walk the learners from the red
   summary to the exact failing step.
2. Diagnose a YAML indentation error and a wrong-event error.
3. Turn on step debug logging and re-run, showing the extra detail.
4. Fix a missing `permissions` failure and a missing-secret failure.
5. Use `gh run view --log-failed` to read just the failing logs from the
   terminal.

Pair this with the [contexts and expressions](../../cheat-sheets/contexts-expressions.md)
and [artifacts and caching](../../cheat-sheets/artifacts-caching.md) cheat sheets.
