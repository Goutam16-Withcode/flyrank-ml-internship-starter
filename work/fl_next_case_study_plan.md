# AI Fluency — Portfolio Maintenance & Next Case Study Protocol

- **Author:** Goutam (FlyRank Intern)
- **Track:** AI Fluency — Portfolio Scalability & Case Study Maintenance (`CUSTOM-MQX0QS1O-B788D1AA`)
- **Date:** 2026-08-20

---

## 1. Concrete Workflow: How to Add the Next Case Study

To add a new project to the portfolio without friction, follow these 4 steps:

1. **Open Existing Claude Project**: Open standing `FlyRank ML Portfolio Build` project in Claude (preserves voice card, technical stack, and profile).
2. **Conversation Input (Messy Draft)**: Type the raw project notes into Claude answering 3 questions:
   - What was the specific business/technical problem?
   - What decisions, feature choices, and split designs did I make?
   - What were the empirical metrics/outcomes (Precision@K, lift over baseline)?
3. **Generate 3-Beat Case Study**: Request Claude to format the response using our standard 3-beat structure:
   - **Beat 1**: The Problem
   - **Beat 2**: What I Did & Decided
   - **Beat 3**: What Came of It
4. **Publish**: Add the generated Markdown block into `work/capstone_report.md` and commit to GitHub.

---

## 2. Named Next Real Piece of Work

- **Next Project Name**: *Real-Time Search Keyword Drift & Cannibalization Detector*
- **Description**: An automated pipeline querying the HuggingFace `FlyRank/internship-warehouse` (~79M rows) via DuckDB to identify keyword cannibalization across client URLs.
- **Target Metrics**: Compute Jaccard overlap between ranking URLs per keyword cluster and flag cannibalized URL pairs.

---

## 3. Evidence of Reminder Set

- **Reminder Schedule**: Monthly Portfolio Maintenance Nudge set for the **1st of every month at 10:00 AM**.
- **Reminder Platform**: Google Calendar & Local Task Manager (`"Audit ML projects & add new case study to portfolio repo"`).
- **Status**: Active recurring event configured.

---

## 4. Preserved Build Context Confirmation

- **Claude Project ID**: `FlyRank ML Portfolio Build`
- **Standing Voice Card**: *"Direct, technical, plain, precise, zero corporate fluff."*
- **Preserved Identity**: Goutam — ML Intern & Systems Developer specializing in reproducible search intelligence and zero-leakage validation rigor.
