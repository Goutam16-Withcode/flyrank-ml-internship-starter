# AI Fluency — Design Judgment, Visual Identity & Image Curation

- **Author:** Goutam (FlyRank ML Intern)
- **Track:** AI Fluency — Visual System & Asset Curation Audit (`CUSTOM-MQWZZ5MU-01C90211`)
- **Date:** 2026-08-20

---

## 1. Visual Identity & Design System Tokens

To ensure the portfolio design frames the technical work without upstaging it, we establish a clean, dark-mode design system:

| Design Token | Selection | Rationale |
|---|---|---|
| **Typography** | Inter / JetBrains Mono | Inter for clean prose readability; JetBrains Mono for metrics, code snippets, and JSON outputs. |
| **Color Palette** | Slate Dark (`#0F172A`), Teal Accent (`#14B8A6`), Pure White (`#F8FAFC`) | Low-contrast dark background reduces fatigue; high-contrast teal accents highlight Precision@50 metrics. |
| **Layout Rule** | Single-column technical flow | Avoids multi-column distraction; keeps reader focused on problem → code → result beats. |
| **Framing Rule** | 1px subtle borders (`#1E293B`) | Clean card containers isolate code blocks without decorative shadows or gradients. |

---

## 2. Design Judgment: AI Image vs Real Technical Screenshots

We evaluate generated AI graphics against real execution screenshots to determine what best serves technical proof:

```text
  [Generative AI Art]  --->  REJECTED  (Abstract, non-verifiable hype image)
  [Real Code Screenshot] --->  APPROVED  (Empirical proof: Terminal logs, Precision@50 metrics, ROC curves)
```

### Curation Audit Table

| Asset Type | Content Description | Decision | Judgment Rationale |
|---|---|---|---|
| **Generated AI Image** | Abstract glowing 3D brain with futuristic circuit lines. | **REJECTED** | Looks like stock hype; fails to prove technical coding competence. |
| **Generated AI Image** | Futuristic robot typing on a glowing laptop. | **REJECTED** | Adds visual clutter; distracts from real data science metrics. |
| **Real Screenshot** | Terminal stdout showing `Random Forest Precision@50: 0.740 (3.08x lift)`. | **APPROVED** | Serves as hard empirical proof that the python pipeline executed cleanly. |
| **Real Chart SVG** | Bivariate correlation bar chart of top ranking signals (`days_since_last_update`). | **APPROVED** | Directly illustrates findings discussed in the research paper methodology. |
| **Real Code Snippet** | `GroupShuffleSplit(n_splits=1, test_size=0.2)` python function. | **APPROVED** | Proves zero-leakage client holdout validation design to technical reviewers. |

---

## 3. The Visual Curation Rule of Thumb

> **Rule**: *"Never use a generated AI image when a real code snippet, terminal log, or data visualization chart can state the proof directly."*
