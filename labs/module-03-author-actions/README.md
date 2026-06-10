# Module 03 - Author and maintain actions

**Domain 3.0 (15%) | Certy lesson: building-actions**
**Practice repo:** [gh200-custom-actions-lab](https://github.com/CertyPro/gh200-custom-actions-lab)

This module moves learners from using actions to building their own. The custom
actions lab has scaffolding for all three action types.

## Concepts to teach

- **The three action types:**
  - **Composite** - bundles several steps, `runs.using: "composite"`. Easiest,
    pure YAML plus shell.
  - **JavaScript** - runs directly on the runner, `runs.using: "node20"`, uses the
    `@actions/core` and `@actions/github` toolkit. Fast, cross-platform.
  - **Docker (container)** - `runs.using: "docker"` with a Dockerfile or image.
    Most control over the environment, Linux runners only, slower to start.
- **The metadata file (`action.yml`):** `name`, `description`, `inputs`,
  `outputs`, `runs`. This file defines the action's contract.
- **Inputs and outputs:** read inputs from `with:` (exposed as `INPUT_*`), set
  outputs by writing `name=value` to the `$GITHUB_OUTPUT` file.
- **Versioning and publishing:** tag releases (`v1.2.3`), keep a moving major tag
  (`v1`), and publish to the GitHub Marketplace. Explain why callers should pin to
  a SHA.
- **Maintenance:** changelogs, GitHub releases, and keeping the action's own
  dependencies up to date.

## Common mistakes

- Choosing a Docker action when a composite or JavaScript action would be simpler
  and faster.
- Setting outputs the old way instead of writing to `$GITHUB_OUTPUT`.
- Forgetting to commit the built `dist/` bundle for a JavaScript action (it runs
  the committed code, not your `node_modules`).
- Missing `description` on inputs, which the Marketplace requires.
- Never moving the major tag, so consumers using `@v1` never get fixes.
- Assuming a Docker action runs on Windows or macOS runners - it does not.

## What to demo live

1. In gh200-custom-actions-lab, write a composite action with two steps that takes
   an input and sets an output.
2. Use that action from a workflow in the same repo.
3. Build a small JavaScript action with `@actions/core` reading an input and
   calling `core.setOutput`.
4. Build a Docker action with a tiny Dockerfile and show it run on an Ubuntu
   runner.
5. Tag a release and move the `v1` tag to demonstrate versioning.

Pair this with the [workflow syntax](../../cheat-sheets/workflow-syntax.md) and
[security](../../cheat-sheets/security.md) cheat sheets (for SHA pinning).
