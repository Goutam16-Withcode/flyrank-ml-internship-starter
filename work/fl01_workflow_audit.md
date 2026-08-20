# FL-01 — Personal Workflow Audit & Toolkit Setup

- **Author:** Goutam (FlyRank Intern)
- **Track:** AI Fluency Track — Task-Classification & Workflow Audit
- **Date:** 2026-08-20

---

## 1. Personal Workflow Audit (12 Recurring Tasks)

Based on Ethan Mollick's *On-Boarding Your AI Intern* framework, the following table audits 12 recurring tasks across study, software development, and side projects:

| # | Recurring Task | Classification | Rationale |
|---|---|---|---|
| 1 | **Original Code Architecture Design** | `Just me` | High-level system design requires human judgment, domain constraints, and trade-off decisions. |
| 2 | **Final Editorial Code Review** | `Just me` | Human oversight is mandatory for security, safety, and verifying business logic before production. |
| 3 | **Boilerplate Code & Skeleton Generation** | `Collaborate with AI` | AI speeds up writing initial setup code, data schemas, and boilerplate functions. |
| 4 | **Data Contract & Schema Validation** | `Delegate to AI with review` | AI generates validation rules and type-checks quickly; human reviews edge cases. |
| 5 | **Bug Diagnosis & Error Stack Trace Analysis** | `Collaborate with AI` | AI rapidly parses long tracebacks and suggests diagnostic root causes. |
| 6 | **Exploratory Data Analysis (EDA) Scripting** | `Collaborate with AI` | AI generates summary statistical code and plotting snippets for quick dataset profiling. |
| 7 | **Technical Documentation & Docstrings** | `Delegate to AI with review` | AI extracts docstrings and writes markdown documentation from clean code. |
| 8 | **Unit Test Suite Generation** | `Collaborate with AI` | AI writes boundary test cases and mock data fixtures to improve test coverage. |
| 9 | **Weekly Research Paper Summarization** | `Delegate to AI with review` | AI extracts key methodology and findings into a 5-bullet summary for fast reading. |
| 10 | **Refactoring Python Helper Functions** | `Collaborate with AI` | AI suggests cleaner list comprehensions and vectorizations; human tests speed. |
| 11 | **CI/CD Build Pipeline Log Inspection** | `Fully automate` | Automated scripts parse build logs and flag failing step errors automatically. |
| 12 | **Dataset CSV Cleaning & Renaming** | `Fully automate` | Scripted pipeline handles column renaming, string trimming, and type casting without intervention. |

---

## 2. Toolkit & Anthropic Academy Setup

- **Tool Accounts Configured**:
  - **Claude (Anthropic)**: Configured free account for reasoning and technical write-ups.
  - **ChatGPT (OpenAI)**: Active account for code generation and alternative syntax checks.
  - **Anthropic Academy**: Enrolled in *AI Fluency: Framework & Foundations* (Module 1 completed).

---

## 3. Claude Project Configuration & Custom Instructions

- **User Profile**: Machine Learning Intern & Full-Stack Developer specializing in Python, data science, and web applications.
- **Tone Preferences**: Professional, concise, technical, and objective. Avoid filler phrases and unnecessary fluff.
- **Current Goals**: Master applied machine learning workflows, model validation, and AI collaboration frameworks.

---

## 4. Target Tasks for FL-02 through FL-04 & Success Definitions

We select three recurring tasks from the audit to reuse in FL-02, FL-03, and FL-04:

### Target Task 1: Exploratory Data Analysis & Signal Profiling (FL-02 Target)
- **Description**: Generating pandas EDA scripts to compute distributions, correlations, and null checks on raw datasets.
- **Definition of "Done Well"**:
  - Computes exact summary statistics (mean, median, null count, correlation) without code syntax errors.
  - Generates clear visualization plots with properly labeled axes and legends.
  - Completes data profiling in <2 minutes vs 15 minutes manually.

### Target Task 2: Automated Unit & Edge Case Test Suite Generation (FL-03 Target)
- **Description**: Writing pytest test functions covering boundary values, empty inputs, and invalid types.
- **Definition of "Done Well"**:
  - Achieves >90% code coverage on target helper functions.
  - Includes tests for edge cases (NaNs, empty strings, zero division).
  - All generated tests pass cleanly on the reference codebase without false failures.

### Target Task 3: Technical Documentation & Report Drafting (FL-04 Target)
- **Description**: Synthesizing pipeline metrics into Markdown reports for technical stakeholders.
- **Definition of "Done Well"**:
  - Accurately captures model precision, recall, baseline comparison, and key feature importances.
  - Uses strictly public-safe, decision-support language with no unverified causal claims.
  - Produces a clear, standard GFM (GitHub Flavored Markdown) report ready for publication.
