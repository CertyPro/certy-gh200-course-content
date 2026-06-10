# Capstone: the GH-200 CI/CD Pipeline Challenge

The final project for the GitHub Actions (GH-200) course. It pulls every exam
domain into one **verifiable** project: a real repository with a working,
hardened CI/CD pipeline.

> Do not just memorise Actions. Ship a pipeline.

## What you will build

A public repository (start from the
[student actions lab](https://github.com/CertyPro/gh200-student-actions-lab)
template, or your own small app) with a complete, secure automation setup.

## The checklist

Work through these in order. Each maps to one or more exam domains.

- [ ] A **CI workflow** that runs on push and pull request: checkout, set up Node,
      install, test - domain 1.0
- [ ] A **matrix** across at least two Node versions - domain 1.0
- [ ] **Dependency caching** so repeat runs are faster - domain 5.0
- [ ] **Job outputs** passed to a downstream job with `needs` - domain 2.0
- [ ] A **custom action** you built (composite, JavaScript, or Docker) and call
      from a workflow - domain 3.0
- [ ] A **reusable workflow** called from the
      [reusable workflows library](https://github.com/CertyPro/gh200-reusable-workflows-library)
      with `uses:` and inputs - domains 1.0 / 4.0
- [ ] A **release workflow** triggered on a `v*` tag - domain 1.0
- [ ] **Least-privilege** `permissions:` on every workflow (read by default, write
      only where needed) - domain 5.0
- [ ] Third-party actions **pinned to a full commit SHA** - domain 5.0
- [ ] An **environment** with a required reviewer protecting a deploy job - domain 5.0
- [ ] A **Dependabot** config keeping actions (and dependencies) up to date - domain 5.0
- [ ] A short **runner and cost note**: which runner you chose and why, and one way
      you would control Actions spend at scale - domain 4.0

## How to submit

Gather these as your proof and submit them wherever your cohort or the Certy
course asks:

```text
Repository URL:     https://github.com/<your-username>/<your-repo>
Green Actions run:  https://github.com/<your-username>/<your-repo>/actions/runs/<id>
Release URL:        https://github.com/<your-username>/<your-repo>/releases/tag/v0.1.0
Security note:      a short paragraph on the permissions, SHA pinning, environment,
                    and Dependabot choices you made
```

## Why this matters

A green pipeline you built and hardened yourself is far stronger evidence than a
passing multiple-choice score. It is also a portfolio piece you can show an
employer.

## Where to get help

- Re-read the relevant [exam objective](../exam-objectives.md) and
  [cheat sheets](../cheat-sheets/).
- Revisit the matching practice repo for each step (linked above).
- Ask in [Discussions](https://github.com/CertyPro/certy-gh200-course-content/discussions).
