---
layout: page
title: "Final Project Rules"
subtitle: "Complete rulebook for Advanced Programming Spring 2025"
---

# FINAL-PROJECT RULEBOOK
MSc Advanced Programming · Spring 2025 UNIL

> **These rules are CONTRACTUAL.** Your GitHub repository, written report, and live demo are the
> graded deliverables for this course --- **none are optional**.

---

## 0 · Quick Index
1. [Scope & Allowed Project Types](#1-scope--allowed-project-types)
2. [Team Formation & Registration](#2-team-formation--registration)
3. [Deliverables](#3-deliverables)
4. [Technical Requirements](#4-technical-requirements)
5. [Milestones & Calendar](#5-milestones--calendar)
6. [Grading Rubric](#6-grading-rubric)
7. [AI-Tool Usage](#7-ai-tool-usage)
8. [Academic Honesty & Licensing](#8-academic-honesty--licensing)
9. [Submission & Late Policy](#9-submission--late-policy)
10. [Support & Escalation](#10-support--escalation)

---

## 1 · Scope & Allowed Project Types
### 1.1 Template Projects (default)
You may choose **one** of the official template repositories listed in the
_global README_ (e.g. **SIMCLT**, **ECONGAMES**).
*Each template already contains a skeleton package, smoke tests, and CI pipeline.*

### 1.2 Solo “Free-Topic” Project   *(OPTIONAL)*
* Work **alone** (no teammates).
* Topic may be _anything in software engineering_ **except** data-science centric
  work.
  **Forbidden:** projects whose *primary* goal is to ingest a dataset, fit/compare statistical or ML models, and produce metrics/plots.
  **Allowed:** simulations, games, CLI and GUI tools, solutions to computational challenges (although must be preapproved).
* Must satisfy **all** rules below.
* **One-paragraph proposal** due **Week 2 Friday 23:59 CET** for Anna's approval.

---

## 2 · Team Formation & Registration
| Item | Requirement |
|------|-------------|
| Team size | 3–4 students for template projects. Solo only for free-topic. |
| Cross-discipline | Mixed econ/actuarial/finance/etc teams encouraged. |
| Registration | Submit GitHub repository URL (or solo proposal) in Moodle **“Projects → Team registration”** by **Week 2 Friday 23:59 CET**. |
| Lock-in | After deadline, teams & project choices are frozen. No swaps (unless in a extreme situation, MUST be escalated with Anna) |

---

## 3 · Deliverables (all **mandatory** – no partial credit)

| # | Item | Description | Deadline / Channel |
|---|------|-------------|--------------------|
| **1** | **GitHub repository** tagged **`v1.0.0`** | Complete, tested, installable package in the course organisation (private team repo). | **Week&nbsp;10 &nbsp;·&nbsp; Fri&nbsp;23:59&nbsp;CET** |
| **2** | **Technical Report** (PDF, 3–4 pages) | Architecture, maths/algorithms, validation, division-of-labour, AI-log summary. | E-mail to **ta-projects@uni-xyz.ch** (exact date announced Week 9) |
| **3** | **Live demo** (15 min) | Run CLI/API, show tests passing, answer viva questions. | In-class, **Week 11** practical session |

---

### 3.1 · GitHub repository requirements

* **Code-freeze tag**: annotated release **`v1.0.0`** on `main`; CI must be green at that commit.
* **Installability**: `pip install .[dev]` works on a fresh clone.
* **Structure**: keep scaffold layout `src/`, `tests/`, `pyproject.toml`, `README.md`, `LICENSE`.
* **Quality gates**
  * `pytest -q --cov=<pkg> --cov-fail-under=90` (≥ 90 % coverage)
  * `mypy --strict src/` passes
  * `flake8` passes
  * code formatted with **black**
* **CI / CD workflow** must: lint → type-check → test → build wheels → upload to **TestPyPI** on tag push.
* **Docs**: Sphinx HTML deployed via GitHub Pages and linked in README.
* **Mandatory files** at the tag
  * `AI_LOG.md` (prompts kept)
  * `NOTICE.md` (licenses / attributions)
  * `sample_data/` (minimal dataset for smoke tests)
* **Licensing**: only MIT / BSD / Apache dependencies.
* **Branch protection**: merging to `main` requires green CI.

> The instructors will clone the repo at `v1.0.0`, run `pip install .[dev]`, `pytest`, and your CLI example.
> Any failure ⇒ **0 pts for repository component**.

---

### 3.2 · Technical Report (PDF, 4-6 pages)

| Section | Content |
|---------|---------|
| **1&nbsp;· Executive summary** | ≈ 150 words: purpose, key results, target user. |
| **2&nbsp;· System architecture** | Folder diagram + short narrative; list external libs. |
| **3&nbsp;· Mathematics / algorithms** | Formulas with variable definitions; cite sources. |
| **4&nbsp;· Validation & testing** | Methods, one table of expected vs. actual results. |
| **5&nbsp;· Division of labour** | Table mapping member → files/features/tests/docs. |
| **6&nbsp;· AI-tool usage summary** | Aggregate stats; reflect on usefulness / risks (link to `AI_LOG.md`). |

*Format:* single-column, 11 pt, ≤ 6 pages incl. figures.
*Filename:* `teamname_project.pdf`

---

### 3.3 · Live demo (15 minutes)

| Segment | Checklist |
|---------|-----------|
| Intro  | Project goal, team members, show tag `v1.0.0`. |
| Run software | *CLI/API on sample data* → show output.<br>*`pytest -q`* → coverage line visible. |
| Highlight | One feature / edge case / performance win. |
| Q & A | Be ready to discuss code, maths, AI-generated parts. |

* Bring your own laptop; have wheel, sample data, and report **offline**.
* Terminal font ≥ 16 pt; rehearse – over-runs will be cut.

---

> **Remember:** repository, report **and** demo are all compulsory.
> Miss one ⇒ automatic fail for the project component.


---

## 4 · Technical Requirements

| Area | Hard Rule |
|------|-----------|
| **Language / Version** | Python >= 3.10 |
| **Repo layout** | Must follow scaffold: `src/`, `tests/`, `pyproject.toml`, `README.md`.<br>**No Jupyter notebooks.** |
| **Coding standards** | `black` formatting, `flake8` lint clean, **`mypy --strict`** passes. |
| **Testing** | Unit + property tests, **≥ 80 % coverage by Week 6, ≥ 90 % final** (`pytest --cov-fail-under`). |
| **CI / CD** | GitHub Actions workflow must run on every push & PR.<br>Steps: install, tests, lint, type-check, coverage gate.<br>Build wheels and upload to **TestPyPI** on GitHub Release tags. |
| **Documentation** | • `README.md` quick-start<br>• Docstrings (NumPy style)<br>• Sphinx HTML docs deployed via GitHub Pages. |
| **Branch protection** | `main` branch must be protected: PR + green CI required to merge. |
| **Dependencies** | Pin in `pyproject.toml`; permissive licenses only (MIT/BSD/Apache). |
| **Sample data** | Provide minimal CSV/YAML in `sample_data/` so smoke tests run offline. |
| **AI Log** | Keep `AI_LOG.md` (see §7). |
| **Semantic Versioning** | Use tags `v0.x.y` during development, `v1.0.0` for final release. |

---

## 5 · Milestones & Calendar

<!-- | Week (2025) | Deliverable | Acceptance criteria |
|-------------|-------------|---------------------| -->
<!-- | **2 (Fri 21 Feb)** | Team registration / solo proposal | Repo exists, scaffold installs & smoke tests pass. |
| **4 (Fri 7 Mar)** | Deterministic core | Template projects: maths validated vs. reference values.<br>Solo projects: core feature working, CI green. |
| **6 (Fri 21 Mar)** | Stochastic / advanced engine | Coverage ≥ 80 %; CLI/API stable. |
| **8 (Mon 31 Mar)** | **Code-freeze & tag `v1.0.0`** | CI green, Sphinx docs live, wheels on TestPyPI. |
| **9 (Week of 7 Apr)** | Report + Live demo | PDF on LMS, 5 min presentation. | -->

TBA.

Late submissions → see §9.

---

## 6 · Grading Rubric (100 pts)

| Category | Points | What we look for |
|----------|--------|------------------|
| **Code quality & packaging** | 35 | Clean API, SOLID design, dependency management, semantic versioning. |
| **Statistical / algorithmic correctness** | 25 | Formulae implemented correctly; outputs validated; edge cases handled. |
| **Tests & CI/CD** | 20 | Coverage target met; Actions workflow robust; property tests where appropriate. |
| **Usability & documentation** | 10 | Clear README, helpful CLI `--help`, docstrings, example scripts. |
| **Report & demo** | 10 | Concise write-up, division-of-labour table, confident demo & Q&A. |

Points will be converted to a final grade out of 1 to 6. 0 is reserved for fraud.

---

## 7 · AI Tool Usage

You are encouraged to experiment with AI-powered coding assistants, such as GitHub Copilot (free for students --- visit https://github.com/education/students) , ChatGPT, Google Gemini, Tabnine, Claude Code, Cursor, Codeium, and so on. We will introduce and demo several of these in class.

However, to keep the project review fair and transparent, follow **either** of the
two simple options below --- whichever feels most natural to your workflow:

| Option | What to do | Where |
|--------|------------|-------|
| **A. Commit notes** (recommended) | Mention “AI-assisted” in the commit message whenever you keep a non-trivial block of code suggested by an AI tool. | Git history |
| **B. Short log file** | Add a brief bullet list of major AI-generated snippets you decided to keep. | `AI_LOG.md` (optional, plain list—no table required) |

Things you **do not** need to track:
* Every single prompt or conversation.
* Code that you deleted or rewrote entirely.

During the live demo, be ready to explain any AI-assisted code you kept—just as you would for code you wrote yourself.

Your report should also contain an "AI tools usage" section in the Appendix, where you explain your workflow in plain words.

Academic honesty rules from §8 still apply: the work must remain yours, and external code must respect licensing.


---

## 8 · Academic Honesty & Licensing

* All University plagiarism rules apply.
* You may incorporate external code only if it is **MIT, BSD, or Apache-2.0** licensed and you credit the source in `NOTICE.md`.
* GPL, AGPL, proprietary, or unlicensed code is **forbidden**.
* Solo free-topic projects must be your own original work except for properly credited third-party libraries.

---

## 9 · Submission & Late Policy

| Delay | Penalty |
|-------|---------|
| ≤ 24 h | -10 pts total score |
| 24–48 h | -20 pts |
| > 48 h | Project fails (0 pts) |

*“Submission” means: tagged release **AND** report uploaded.*
Demo slot missed without documented medical reason = fail.

---

## 10 · Support & Escalation

* **Every live session** will have time for a dedicated Q&A.
* *I will not be live debugging your code with you*, but I will try my best to give you high-level advice and resources.
* **Office hours** — TBA (book time by email anna.smirnova@unil.ch at least 48 hours prior!)
* **Issue tracker** — each template repo has issues enabled; use for bug reports or clarifications.
* Urgent private matters → email **anna.smirnova@unil.ch**.

---

> **Remember:** Your repository, report, and demo are *all* mandatory.
> Stay on schedule, keep CI green, and you'll cruise through the assessment.

