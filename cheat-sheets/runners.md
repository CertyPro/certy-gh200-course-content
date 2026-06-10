# Cheat Sheet - Runners

A runner is the machine that executes a job. You choose one with `runs-on`.

## GitHub-hosted vs self-hosted

| | GitHub-hosted | Self-hosted |
| --- | --- | --- |
| Managed by | GitHub | You |
| OS | Ubuntu, Windows, macOS | Anything you install on |
| Pre-installed tools | Large standard toolset | Whatever you install |
| Each job runs on | A clean, fresh VM | Your machine (state can persist) |
| Cost | Billed per minute (free tier on public repos) | Your own hardware and time |
| Best for | Standard builds and tests | Special hardware, private networks, custom tools |

## GitHub-hosted runner labels

```yaml
runs-on: ubuntu-latest
runs-on: ubuntu-24.04
runs-on: windows-latest
runs-on: macos-latest
```

Larger runners (more cores and memory) are configured at the organisation level
and selected by their custom label:

```yaml
runs-on: ubuntu-latest-8-cores   # example custom larger-runner label
```

## Self-hosted runner labels

Self-hosted runners advertise labels. A job is matched when all the labels it
asks for are present.

```yaml
runs-on: [self-hosted, linux, x64, gpu]
```

Default labels include `self-hosted`, the OS (`linux`, `windows`, `macOS`) and
the architecture (`x64`, `arm64`). You can add your own custom labels.

## Runner groups

Runner groups are an **access-control** feature. They decide which repositories
and workflows are allowed to use a set of runners.

- Available for organisations and enterprises.
- A runner belongs to exactly one group.
- A group can be restricted to selected repositories and, optionally, selected
  workflows.

Do not confuse runner **groups** (who may use the runners) with runner
**labels** (how a job selects a runner).

## Key points for the exam

- `runs-on` selects the runner by label or list of labels.
- GitHub-hosted runners give a clean VM per job; self-hosted runners may keep
  state, so clean up after yourself.
- Self-hosted runners are good for private networks and custom hardware but you
  own their security and maintenance.
- Runner groups control access across repos and workflows; configure them at org
  or enterprise level.
- Never run self-hosted runners on public repositories without care, because
  untrusted pull requests could run code on your machine.
