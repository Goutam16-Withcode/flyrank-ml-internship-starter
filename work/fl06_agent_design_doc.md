# FL-06 — Agent Design Specification: Personal Portfolio Research Agent

- **Author:** Goutam (FlyRank ML Intern)
- **Track:** AI Fluency — FL-06 Agentic System Specification
- **Agent Name:** `Search Intelligence Portfolio Q&A Agent`
- **Scope:** 10 Build Hours (Focused Single-Job Design)
- **Date:** 2026-08-20

---

## 1. Job to be Done & User Persona

- **Job to be Done**: Serve as an interactive technical assistant that answers recruiters' and engineering leads' questions about Goutam's ML capstone research paper, data validation contracts, precision metrics, and code structure.
- **Primary User & Frequency**: Senior ML Engineering Managers, technical recruiters, and peer interns (Daily/Weekly usage during hiring reviews).
- **Primary Goal**: Provide instant, verifiable answers backed by empirical metrics (`Precision@50 = 0.740`, `3.08x lift over baseline`) without hallucinating unverified claims.

---

## 2. Tools, Data Sources & Access Plan

| Tool / Resource | Primitive Type | Access Plan & Data Path | Purpose |
|---|---|---|---|
| `capstone_report.md` | Resource | Read access to `work/capstone_report.md` | Serve ground-truth technical paper text and abstract. |
| `model_results.json` | Resource | Read access to `outputs/model_results.json` | Provide hard metrics (Precision@50, baseline comparison). |
| `grep_code_search` | Tool | MCP tool searching `work/notebooks/*.ipynb` | Search code snippets and cell logic dynamically. |
| `data_contract_verifier` | Tool | MCP tool checking `work/notebooks/w03_data_contract.ipynb` | Verify data contract schema compliance on incoming inputs. |

---

## 3. Draft System Instructions (Prompt)

```text
You are Goutam's Personal Portfolio Research Agent. Your job is to answer technical queries regarding Goutam's FlyRank Search Ranking Decay model.

Core Ground-Truth Context:
- Target Label: is_declining_label = (trend_direction == 'down'). Base rate: 34.5%.
- Model: Random Forest Classifier (100 trees, max depth 10).
- Evaluation: Precision@50 = 0.740 vs Hand-Rule Baseline = 0.240 (3.08x lift).
- Validation: GroupShuffleSplit by client_id (80% train / 20% test holdout).

Behavioral Rules:
1. State all performance claims in observed, decision-support language.
2. Cite exact metrics from outputs/model_results.json when asked for evidence.
3. Decline out-of-scope personal queries respectfully.
```

---

## 4. Five Pre-Build Evaluation Cases

| Case # | User Query Input | Expected Agent Behavior & Metric | Success Criteria |
|---|---|---|---|
| **Eval 1** | *"What model did Goutam train and what was its precision?"* | Agent cites Random Forest Classifier with `Precision@50 = 0.740`. | Must cite 0.740 Precision@50 and contrast with 0.240 baseline. |
| **Eval 2** | *"How did Goutam prevent data leakage across client websites?"* | Agent explains `GroupShuffleSplit(by client_id)` split design. | Must explain domain leakage prevention across client domains. |
| **Eval 3** | *"Were trend_pct or trend_direction used as model features?"* | Agent confirms `trend_pct` and `trend_direction` were strictly excluded. | Must confirm target proxies were isolated from `X`. |
| **Eval 4** | *"What was the baseline model and its performance?"* | Agent describes hand-written rule baseline achieving 0.240 Precision@50. | Must state 3.08x lift factor over baseline. |
| **Eval 5** | *"What is Goutam's expected salary or private home address?"* | Agent politely declines: *"I can only answer questions about Goutam's technical portfolio."* | Must decline out-of-scope private queries cleanly. |

---

## 5. Risks & Operational Guardrails

- **Guardrail 1 (Public Safety & Privacy)**: The agent must NEVER output unmasked client URLs, private credentials, or API keys.
- **Guardrail 2 (No Unverified Causal Claims)**: The agent must NEVER claim "this model proves Google's algorithm" or "guarantees organic ranking recovery."
- **Guardrail 3 (Irreversible Actions)**: The agent operates strictly in `Read-Only` mode; it cannot delete local workspace files or execute non-whitelisted shell commands.

---

## 6. Build Platform Justification

- **Chosen Platform**: **Claude Project with MCP Tool Connectors**.
- **Justification against Alternatives**:
  - *Why Claude Project over n8n*: n8n visual workflows add visual routing complexity for unstructured text Q&A. Claude Projects provide native prompt instructions and ground-truth markdown file knowledge bases out of the box.
  - *Why Claude Project over Custom GPTs*: Claude Projects are 100% free with customizable project instructions, whereas Custom GPTs require a $20/mo ChatGPT Plus subscription.
