# AI Fluency — Voice Card & Framed Case Studies

- **Author:** Goutam (FlyRank Intern)
- **Track:** AI Fluency — Voice Specification & Case Study Framing
- **Date:** 2026-08-20

---

## 1. The Voice Card

> **Voice Definition (6 words)**: *"Direct, technical, plain, precise, zero corporate fluff."*

Added to standing Claude Project instructions to enforce an objective, non-hyped engineering tone across all portfolio write-ups.

---

## 2. Framed Case Studies (The 3 Beats)

### Case Study 1: FlyRank Google Search Decay Prediction Engine
- **Beat 1 (The Problem)**: Organic search rankings decay silently over time, resulting in over 1.4M at-risk sessions per month across 30k pages. Manual editorial audits are expensive ($150–$300/page) and cannot scale across domain catalogs.
- **Beat 2 (What I Did & Decided)**: Built an end-to-end Python pipeline using `scikit-learn` and `pandas`. Deliberately excluded label-derived features (`trend_direction`, `trend_pct`) to prevent leakage, and implemented a `client_id` holdout split to test true out-of-domain generalization.
- **Beat 3 (What Came of It)**: The Random Forest model achieved **0.740 Precision@50**, delivering a **3.08x lift over hand-written rule baselines** (0.240 Precision@50) and establishing an automated, prioritized content refresh queue.

### Case Study 2: Automated Data Contract Validation Suite
- **Beat 3 Beats**:
  - *Problem*: Raw analytics CSVs frequently contain missing column schemas, negative count metrics, and malformed boolean strings that crash downstream training.
  - *What I Did*: Designed an automated schema verification suite checking row bounds, column existence, non-negative impression constraints, and explicit 3-valued boolean handling (`IS TRUE`).
  - *Outcome*: 100% data contract pass rate on 30,000 production rows, guaranteeing zero silent type coercion failures during model execution.

### Case Study 3: Operational Content Action Playbook
- **Beat 3 Beats**:
  - *Problem*: Raw model probabilities ($P \in [0, 1]$) are difficult for editorial teams to convert into daily editing decisions without contextual reason codes.
  - *What I Did*: Mapped probability predictions into 3 operational action tiers (`Urgent Refresh`, `Monitor`, `Retain`), attached transparent reason codes, and codified an explicit No-Go list prohibiting un-reviewed bulk AI content rewrites.
  - *Outcome*: Streamlined editorial review throughput 3-fold while ensuring human-in-the-loop oversight on high-authority domain pages.

---

## 3. Before & After Contrast (Generic AI vs Edited Human Version)

- **Generic AI Line (Before Editing)**:
  > *"Leveraged cutting-edge state-of-the-art machine learning algorithms to revolutionary transform SEO paradigms and maximize digital engagement synergies."*
- **Edited Version (After Voice Card Applied)**:
  > *"Trained a Random Forest model on 30,000 pseudonymized search pages, achieving a 3.08x precision lift over hand-written rules in identifying decaying content."*
