# FL-09 & FL-10 — Final Capstone Package, Retrospective & Master Index

- **Author:** Goutam (FlyRank ML & AI Fluency Intern)
- **Track:** AI Fluency & Machine Learning — FL-09 / FL-10 Final Capstone Checkpoint
- **Repository URL:** [`https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter`](https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter)
- **Deployed Capstone Paper:** [`https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter/blob/main/work/capstone_report.md`](https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter/blob/main/work/capstone_report.md)
- **Date:** 2026-08-20

---

## Part 1: FL-09 Documentation & Live Demo Outline

### 1.1 Project Overview & Architecture
The **FlyRank Search Ranking Decay Predictor** is a production-grade machine learning system designed for SEO engineering teams and digital publishers. It processes anonymized organic search analytics across 30,000+ web pages to identify declining search performance before catastrophic traffic loss occurs.

```text
[Raw Search CSV] ---> [Data Contract Validator] ---> [Grouped Split Train/Test] ---> [RF Evaluator]
(30k Pages Analytics)     (Schema & Null Safety)       (Holdout 20% Clients)      (Precision@50: 0.740)
                                                                                         |
[Live Portfolio Site] <--- [Action Playbook Queue] <--- [Report Building Engine] <-------┘
```

### 1.2 Setup Guide for a Stranger (100% Reproducible)
```bash
# 1. Clone the repository
git clone https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter.git
cd flyrank-ml-internship-starter

# 2. Install dependencies
pip install pandas scikit-learn numpy reportlab

# 3. Run the complete pipeline end-to-end
python scripts/run_all.py

# 4. View generated artifacts in work/outputs/
# Outputs include: outputs/model_results.json, outputs/refresh_queue.csv, and outputs/flyrank_refresh_model_results.pdf
```

### 1.3 Evaluation Results & Honest Limitations
- **Evaluation Baseline**: Hand-written rule baseline achieved **0.240 Precision@50**.
- **Random Forest Model**: Achieved **0.740 Precision@50** (a **3.08x empirical lift**).
- **Honest Limitations**:
  1. *Seasonal Traffic False Positives*: Sudden impression drops on seasonal pages (e.g. holiday gift guides) can trigger false decay alerts.
  2. *Cold-Start Pages*: Newly created URLs (<60 days old) lack sufficient historical trends for reliable scoring.

### 1.4 AI Transparency Statement
> *"I designed the pipeline architecture, zero-leakage group validation split, and data contract rules. I utilized AI as a pair programming assistant to accelerate code drafting and syntax formatting, while empirically verifying all model scores, precision metrics, and script outputs myself."*

### 1.5 5-Minute Live Demo Script (No Slides)
- **0:00 - 1:00 (The Problem & Question)**: Introduce the 30k search page dataset and explain why silent ranking decay causes over 1.4M lost sessions per month.
- **1:00 - 2:30 (Live Code Execution & Architecture)**: Run `python scripts/run_all.py` on camera in the terminal. Show `GroupShuffleSplit` by `client_id` in action.
- **2:30 - 3:30 (One Design Decision)**: Explain why standard `train_test_split` causes domain leakage (0.820 vs honest 0.740 Precision@50).
- **3:30 - 4:30 (One Honest Limitation)**: Demonstrate how seasonal traffic dips can flag false positives on seasonal content.
- **4:30 - 5:00 (Action Playbook Output)**: Display `outputs/refresh_queue.csv` and show how top 50 prioritized pages are queued for human review.

---

## Part 2: FL-10 Master Deliverable Index

| Module | Assignment ID | Deliverable Title & Content | Direct Repository Link |
|---|---|---|---|
| **AI Fluency** | `FL-01` | Workflow Audit & Toolkit Setup | [`work/fl01_workflow_audit.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/fl01_workflow_audit.md) |
| **AI Fluency** | `FL-02` | Interactive Prompt Engineering & Cross-Model Audit | [`work/fl02_prompt_iteration_log.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/fl02_prompt_iteration_log.md) |
| **AI Fluency** | `FL-04` | Chained Automation Workflow & Research Pipeline | [`work/fl04_automation_workflow.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/fl04_automation_workflow.md) |
| **AI Fluency** | `FL-05` | Agents vs Workflows & MCP Technical Explainer | [`work/fl05_agents_mcp_explainer.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/fl05_agents_mcp_explainer.md) |
| **AI Fluency** | `FL-06` | Agent Design Specification (Portfolio Q&A Agent) | [`work/fl06_agent_design_doc.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/fl06_agent_design_doc.md) |
| **AI Fluency** | `FL-07` | Working Agent MVP & Iteration Log | [`work/fl07_working_agent_mvp.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/fl07_working_agent_mvp.md) |
| **AI Fluency** | `PF-05` | Web Infrastructure, Deployment & DNS Walkthrough | [`work/fl_web_infrastructure_dns.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/fl_web_infrastructure_dns.md) |
| **AI Fluency** | `FL-CAP` | Personal Brand Website & Portfolio AI Agent Capstone | [`work/fl_capstone_personal_brand_agent.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/fl_capstone_personal_brand_agent.md) |
| **ML Track** | `ML-01 to ML-07` | Guided Notebooks & Signal Audits | [`work/notebooks/`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/notebooks/) |
| **ML Track** | `ML-CAP-01` | Final Research Paper & Capstone Report | [`work/capstone_report.md`](file:///e:/flyrank-ml-internship-starter/flyrank-ml-internship-starter/work/capstone_report.md) |

---

## Part 3: 650-Word Retrospective (Written for Week 1 Self)

> **Dear Week 1 Self,**
> 
> When you first started this internship, you thought machine learning engineering was about pulling complex neural network libraries from HuggingFace and aiming for a high accuracy score on a generic dataset. You assumed AI tools were just faster search engines for copying code snippets. 
> 
> Eight weeks later, your entire mental model of software engineering has fundamentally shifted.
> 
> ### What Changed in How I Work
> In Week 1, you would have taken a 30,000-row CSV file, split it randomly with `train_test_split(test_size=0.2)`, trained a model, seen an 85% accuracy number, and declared victory. You would not have asked where the label came from, whether pages belonged to the same client domain, or if feature columns contained hidden label proxies.
> 
> Today, you don't touch a model until you've written an automated data contract (`03_data_contract.ipynb`) and audited every single feature for target leakage. You learned that standard random splitting cheats by leaking domain authority quirks between training and testing sets. By forcing a `GroupShuffleSplit` by `client_id`, you accepted a lower, honest score (**0.740 Precision@50**)—because an honest score on unseen domains is the only metric that matters in production.
> 
> ### The Three Most Transferable Things I Learned
> 1. **Zero-Leakage Validation Rigor**: High model evaluation scores built on target leakage or client domain overlap are a dangerous illusion. Always group holdouts by entity (`client_id`) and audit feature vectors to ensure label proxy variables (`trend_direction`, `trend_pct`) are strictly isolated.
> 2. **AI as a System Builder, Not an Author**: The gap between lazy single prompts and engineered workflows is huge. By structuring clear constraints, role assignments, step decomposition, and MCP tool connections, you turn AI from a chat widget into a deterministic engineering asset.
> 3. **Honesty as Credibility**: Employers and reviewers don't trust flawless marketing hype. They trust engineers who know exactly where their system breaks. Explaining your model's limitations (such as seasonal traffic false positives) builds far more trust than claiming your model is infallible.
> 
> ### What I Would Build Next
> Next, I will build an automated keyword cannibalization detector that queries the 79M-row FlyRank warehouse via DuckDB. It will calculate Jaccard content overlap across client URLs in real-time, integrating with a live API backend.
> 
> Keep building with rigor, verifying every receipt, and shipping out in the open.
> 
> *— Goutam (Week 8)*

---

## Part 4: Verified Hours Log & Build-in-Public Post

### Internship Verified Hours Log
- **Total Hours Completed**: **52 Hours** across 8 Weeks.
- **Breakdown**: 24 Hours Notebook Modeling & Feature Engineering + 16 Hours Pipeline Automation & PDF Build + 12 Hours Web Infrastructure & Agent Design + 00 Hours Final Paper Deployment.
- **Verification Status**: Complete & Verified.

---

### Build-in-Public Social Post (Employer-Facing Summary)

> 🚀 **Shipped my FlyRank ML Internship Capstone Research Paper & Agent Portfolio!**
> 
> Over the past 8 weeks, I built an end-to-end Machine Learning system that predicts organic search ranking decay across 30,000+ anonymized web pages.
> 
> 📊 **Key Engineering Results**:
> • **3.08x Precision Lift**: Random Forest model achieved **0.740 Precision@50** vs **0.240** for rule baselines.
> • **Zero-Leakage Rigor**: Validated via `GroupShuffleSplit` by `client_id` to test true out-of-domain generalization.
> • **Automated Action Playbook**: Generates prioritized content refresh queues with reason codes and automated PDF reporting.
> 
> 💡 **Key Decision**: I intentionally excluded label proxies (`trend_pct`) and grouped client holdouts to ensure honest evaluation on unseen domains.
> ⚠️ **Known Limitation**: Seasonal traffic drops can occasionally trigger false decay flags, which is why all outputs feed into a human-in-the-loop review queue.
> 
> 🔗 **Read the full research paper & code repo**:  
> `https://github.com/Goutam16-Withcode/flyrank-ml-internship-starter`
> 
> #MachineLearning #DataScience #FlyRankAI #AI #Python #BuildInPublic
