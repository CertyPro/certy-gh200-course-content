# Certy GH-200 Course Content

**Automate with confidence - pass GH-200 and build real CI/CD skill.**

This is the teaching hub for the GitHub Actions certification (**GH-200**) on the
[Certy](https://certy.pro) learning platform. It holds the exam-objective map,
lesson notes, lab walkthroughs, cheat sheets, practice questions, a glossary and
a video roadmap. Everything here is mapped to the real GH-200 exam domains so you
can study with confidence and finish with skills you can use at work.

GH-200 is GitHub's "GitHub Actions" certification, validated through Microsoft
Learn. It tests whether you can author and manage workflows, consume and
troubleshoot them, build and maintain actions, administer Actions across an
enterprise, and secure and optimise your automation.

---

## The repo set

Certy ships GH-200 as a hub plus a set of focused, hands-on practice repos. Each
practice repo lets you do the work, not just read about it. Clone the one that
matches the domain you are studying.

| Repo | What it is for | Domain(s) served |
| --- | --- | --- |
| [certy-gh200-course-content](https://github.com/CertyPro/certy-gh200-course-content) | This repo - the teaching hub: objectives, notes, cheat sheets, questions, glossary | All |
| [gh200-student-actions-lab](https://github.com/CertyPro/gh200-student-actions-lab) | Guided exercises to author your first workflows and harden them | 1.0, 5.0 |
| [gh200-broken-workflows](https://github.com/CertyPro/gh200-broken-workflows) | Deliberately broken workflows to read logs and fix | 2.0 |
| [gh200-custom-actions-lab](https://github.com/CertyPro/gh200-custom-actions-lab) | Build composite, JavaScript and Docker actions from scratch | 3.0 |
| [gh200-enterprise-admin-sim](https://github.com/CertyPro/gh200-enterprise-admin-sim) | Simulated org and enterprise admin: policies, runner groups, required workflows | 4.0 |
| [gh200-security-challenges](https://github.com/CertyPro/gh200-security-challenges) | Token scopes, secrets, OIDC and supply-chain hardening tasks | 5.0 |
| [gh200-reusable-workflows-library](https://github.com/CertyPro/gh200-reusable-workflows-library) | A library of reusable workflows to call, study and reuse | 1.0, 4.0 |

---

## How to use this course

1. Start with [`exam-objectives.md`](exam-objectives.md) to see the five domains,
   their exam weights and exactly which skills each one tests.
2. Work through the modules in [`labs/`](labs/). Each module pairs lesson notes
   with a hands-on practice repo from the table above.
3. Keep the [`cheat-sheets/`](cheat-sheets/) open while you practise. They are
   quick references for syntax, contexts, runners, caching, reusable workflows
   and security.
4. Test yourself with [`practice-questions/`](practice-questions/), then take the
   full weighted mock exam.
5. Look up anything unfamiliar in the [`glossary/`](glossary/).

The free course and the full mock exam (25 questions, 70% to pass, weighted like
the real GH-200) live at **[certy.pro](https://certy.pro)**.

---

## What is in this repo

- [`exam-objectives.md`](exam-objectives.md) - the five domains with weights,
  "you should be able to" skill lists, and the matching lesson and practice repo.
- [`video-roadmap.md`](video-roadmap.md) - the planned video series, one per
  module, with Certy slugs and recording notes.
- [`labs/`](labs/) - instructor-facing walkthrough notes for each of the five
  modules.
- [`cheat-sheets/`](cheat-sheets/) - concise references: workflow syntax,
  contexts and expressions, runners, artifacts and caching, reusable workflows,
  security.
- [`practice-questions/`](practice-questions/) - sample questions with answers
  plus a link to the full mock exam.
- [`glossary/`](glossary/) - key GH-200 terms in plain English.
- [`resources/`](resources/) - official documentation and certification links.
- [`challenge-project/`](challenge-project/) - the **GH-200 CI/CD Capstone**: build
  and harden a complete pipeline that touches every domain, with verifiable proof.

---

## Exam at a glance

| Domain | Title | Weight |
| --- | --- | --- |
| 1.0 | Author and manage workflows | 25% |
| 2.0 | Consume and troubleshoot workflows | 20% |
| 3.0 | Author and maintain actions | 15% |
| 4.0 | Manage GitHub Actions for the enterprise | 27% |
| 5.0 | Secure and optimise automation | 13% |

Domain 4.0 carries the most weight, so do not skip the enterprise material.

---

## Licensing

- **Code and snippets:** [MIT](LICENSE).
- **Learning content (prose):** [CC-BY-4.0](LICENSE-CONTENT.md), with attribution
  to Certy (Coded Vision Design).

See [`LICENSE`](LICENSE) and [`LICENSE-CONTENT.md`](LICENSE-CONTENT.md) for the
full terms.

---

Built and maintained by [Certy](https://certy.pro) - Coded Vision Design.
Org: [github.com/CertyPro](https://github.com/CertyPro).
