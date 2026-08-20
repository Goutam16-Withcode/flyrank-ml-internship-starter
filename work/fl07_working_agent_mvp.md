# FL-07 — Build Checkpoint 1: Working Agent MVP & Iteration Log

- **Author:** Goutam (FlyRank ML Intern)
- **Track:** AI Fluency — FL-07 Working Agent MVP Implementation
- **Agent Name:** `Search Intelligence Portfolio Q&A Agent (v1.0 MVP)`
- **Live Tool Connections**: Local File System MCP Connector (`view_file`, `read_json`, `grep_search`)
- **Date:** 2026-08-20

---

## 1. Live Tool Connection Architecture

```text
[User Prompt] ---> [Claude Project Agent Persona] ---> [MCP Tool Call: view_file / read_json]
                                                                |
                                                      [Local Workspace File]
                                                                |
[Formatted Answer] <--- [Ground-Truth Citation] <--- [Parsed JSON / Markdown Receipts]
```

---

## 2. Iterative Build Log

| Iteration Phase | What Was Attempted | What Broke | Action Taken / Fix | Spec Deviation & Rationale |
|---|---|---|---|---|
| **Phase 1: Initial Prompt** | Loading entire raw `content_refresh_anonymized.csv` (30k rows) directly into context. | Exceeded token limits and caused latency (>30 seconds). | Switched to passive MCP tool loading: agent uses `view_file` to query `model_results.json` on-demand. | **Cut from Spec**: Raw CSV loading cut in favor of pre-computed metrics JSON receipts to maintain sub-second response times. |
| **Phase 2: Tool Schema** | Connecting custom python script wrapper for metric retrieval. | Script invocation threw path resolution errors on Windows environments. | Replaced custom wrapper script with native MCP `read_json` tool. | Simplified tool stack to native MCP tools for 100% platform portability. |
| **Phase 3: Metric Accuracy** | Agent hallucinated `0.850` precision on ungrounded prompts. | Unconstrained prompt allowed speculative extrapolation. | Hardcoded strict system instruction: *"Only state precision metrics after reading `outputs/model_results.json`."* | Added mandatory pre-response tool check rule. |

---

## 3. End-to-End Execution Demo Log (Raw Run Capture)

### Test Run: Recruiter Metric Verification

- **User Request**:
  > *"Can you verify Goutam's Random Forest model performance on the test set and explain how he prevented data leakage across client domains?"*

- **Agent Tool Calls Executed**:
  1. `read_json(path="outputs/model_results.json")` -> Returned `random_forest: precision_at_50 = 0.740`, `baseline: 0.240`.
  2. `view_file(path="work/capstone_report.md", StartLine=40, EndLine=60)` -> Parsed GroupShuffleSplit by `client_id` section.

- **Final Formatted Response Generated**:
  > *"Goutam's Random Forest model achieved a **Precision@50 of 0.740** on the client-holdout test set, representing a **3.08x lift** over the hand-written rule baseline (0.240 Precision@50).*
  > 
  > *To prevent data leakage across client domains, Goutam implemented a `GroupShuffleSplit` by `client_id` (80% train / 20% test holdout). This ensures zero client domain overlap between training and testing sets, validating true out-of-domain model generalization."*

---

## 4. MVP Verification Checklist

- [x] Agent completes core job end-to-end without manual mid-run editing.
- [x] Live MCP tool connections active (`read_json`, `view_file`).
- [x] Build log documents real technical iteration and spec cuts.
- [x] Unedited end-to-end execution run log documented.
