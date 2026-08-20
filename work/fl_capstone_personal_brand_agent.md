# General AI Fluency Capstone — Personal Brand Website & Personal AI Agent

- **Author:** Goutam (FlyRank ML Intern)
- **Project:** Personal Engineering Portfolio Website & Recruiter Q&A AI Agent
- **Track:** AI Fluency Capstone (`fl-cap`)
- **Date:** 2026-08-20

---

## 1. Executive Summary & Project Brief

This capstone project ships a high-performance personal engineering brand website integrated with an interactive **Personal Portfolio AI Agent**. The platform presents empirical machine learning research (including the FlyRank Search Ranking Decay model), demonstrates out-of-domain model validation rigor, and allows recruiters/technical leads to query project metrics via an AI assistant.

---

## 2. System Architecture & Tech Stack

```text
[Visitor / Recruiter]  --->  [Vanilla JS Frontend UI]  --->  [Personal AI Agent Engine]
                                    |                                 |
                            (Modern Dark Mode UI)           (System Prompt Persona)
                                    |                                 |
                          [Portfolio Case Studies]         [Capstone Metrics Context]
```

### Technology Stack
- **Frontend Architecture**: HTML5, Vanilla CSS (Modern Dark Mode with glassmorphism design), Vanilla JavaScript.
- **AI Agent Engine**: Claude 3.5 / OpenAI API integration with system prompt persona and custom portfolio knowledge base.
- **Backend / Deployment**: GitHub Pages static site hosting with serverless API edge functions.

---

## 3. Personal AI Agent Specification

### Agent Persona & System Prompt
```text
You are Goutam's Personal Portfolio Assistant. Your role is to answer questions from engineering managers and technical recruiters about Goutam's ML projects, capstone results, and engineering background.

Key Knowledge Base Context:
1. FlyRank Search Decay Model: Random Forest classifier achieving 0.740 Precision@50 (3.08x lift over 0.240 baseline) across 30,000 anonymized pages.
2. Validation Rigor: GroupShuffleSplit by client_id preventing cross-domain leakage. Prohibited feature audit excluding trend_direction and trend_pct.
3. Code Integrity: 100% data contract pass rate on schema validation suite.

Tone: Professional, direct, technical, objective. Always cite concrete metrics (Precision@50, lift factor) when answering project questions.
```

### Sample Interactive Agent Q&A
- **Visitor Query**: *"What model did Goutam train for search decay, and how did he validate it?"*
- **Agent Response**: *"Goutam trained a Random Forest model (100 trees, max depth 10) on 30,000 anonymized pages. To prevent cross-domain data leakage, he validated the model using a GroupShuffleSplit by client_id (80% train / 20% holdout). The model achieved a Precision@50 of 0.740, representing a 3.08x lift over hand-written baseline rules (0.240)."*

---

## 4. Website Sitemap & Core Pages

1. **Hero Banner**: Primary value proposition + Quick Call-to-Action to read the capstone paper.
2. **Featured Case Studies**:
   - *FlyRank Search Decay Predictor* (3.08x Precision@50 lift, Random Forest, Grouped Split).
   - *Data Contract Schema Validator* (Automated 4/4 schema check suite).
   - *Operational Action Playbook* (Top-50 refresh queue with reason codes).
3. **Interactive AI Agent Window**: Embedded chat interface for instant portfolio Q&A.
4. **Technical Background & Skills**: Python, scikit-learn, pandas, SQL, DuckDB, REST APIs.
5. **Contact & Links**: GitHub, LinkedIn, and direct email contact options.

---

## 5. Live Project & Code Links

- **GitHub Repository**: [`https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter`](https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter)
- **Deployed Capstone Paper**: [`https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter/blob/main/work/capstone_report.md`](https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter/blob/main/work/capstone_report.md)
