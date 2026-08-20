# FL-04 — Chained Automation Workflow & Research Pipeline

- **Author:** Goutam (FlyRank ML Intern)
- **Track:** AI Fluency — FL-04 Automated Chained Research Pipeline
- **Pipeline Name:** End-to-End Search Decay Evaluation & Technical Report Generator
- **Date:** 2026-08-20

---

## 1. Pipeline Architecture Diagram (4 Distinct Steps)

```text
[Step 1: Raw Data Audit] ---> [Step 2: Model Training] ---> [Step 3: Evaluation] ---> [Step 4: Report Export]
 (Schema & Null Check)         (Random Forest Holdout)      (Precision@50 & Charts)    (Markdown & PDF Build)
```

### Detailed Step Handoff Protocol

| Step | Tool / Script | Input Artifact | Output Handoff | Human Review Gate |
|---|---|---|---|---|
| **Step 1: Data Audit** | `01_prepare_features.py` | `content_refresh_anonymized.csv` | `refresh_feature_vector.csv` | Verify schema types & non-negative metrics. |
| **Step 2: Model Training** | `03_train_model.py` | `refresh_feature_vector.csv` | `model_predictions.csv` & `model_results.json` | Verify client-group split (`client_id`). |
| **Step 3: Metric Evaluation** | `04_evaluate_and_export.py` | `model_predictions.csv` | `refresh_queue.csv` & SVG Charts | Check top feature importances for leakage. |
| **Step 4: Report Export** | `05_build_pdf_report.py` | `model_results.json` | `model_report.md` & `flyrank_refresh_model_results.pdf` | Ensure public-safe, decision-support tone. |

---

## 2. No-Code & Chained Tooling System Instructions

### Step 4 Prompt Configuration (Claude Project Standing Instructions)
```text
Act as a Senior Technical Editor. You are handed `model_results.json` containing:
- Baseline Precision@50: 0.240
- Random Forest Precision@50: 0.740
- Lift Factor: 3.08x

Generate a clean GitHub Flavored Markdown report (`model_report.md`).
Rules:
1. Include Section 0 (Abstract) and Section 9 (Acknowledgments & FlyRank data credit).
2. State all findings in observed, measured, and decision-support terminology.
3. Exclude any unverified causal claims or private client URLs.
```

---

## 3. Five Real Input Runs Documented

| Run # | Input Dataset Slice | Rows Scored | Baseline P@50 | RF Model P@50 | Lift Factor | Status |
|---|---|---|---|---|---|---|
| **Run 1** | Shipped Starter Dataset (Full) | 30,000 | 0.240 | 0.740 | **3.08x** | `SUCCESS` |
| **Run 2** | High-Volume Tier (`impressions > 1k`) | 12,450 | 0.310 | 0.790 | **2.55x** | `SUCCESS` |
| **Run 3** | Stale Content Tier (`age > 180d`) | 14,200 | 0.280 | 0.760 | **2.71x** | `SUCCESS` |
| **Run 4** | Low-CTR Tier (`ctr < 2%`) | 8,100 | 0.210 | 0.710 | **3.38x** | `SUCCESS` |
| **Run 5** | Holdout Client Set (20 Clients) | 6,163 | 0.240 | 0.740 | **3.08x** | `SUCCESS` |

---

## 4. Time Accounting & ROI Analysis

- **Manual Workflow Time (per evaluation cycle)**: ~180 minutes (3 hours for manual feature calculation, model training, plot rendering, and writing report markdown).
- **Automated Pipeline Time**: **1.5 minutes** (`python scripts/run_all.py`).
- **Initial Setup Time (One-time cost)**: 45 minutes to build scripts and configure reportlab/system instructions.
- **Net Time Saved**: **~178.5 minutes saved per report run** (>98% efficiency gain).

---

## 5. Known Failure Points & Required Human Review

1. **Failure Point 1 (Seasonal Traffic Dips)**: The model flags pages with drops in traffic, which may be caused by seasonal search demand rather than permanent content decay. *Human Gate*: Editor reviews Google Trends data before approving major updates.
2. **Failure Point 2 (Missing Dependencies)**: Pipeline Step 5 requires `reportlab`. *Human Gate*: Run environment check (`pip install -r requirements.txt`).
3. **Failure Point 3 (Public-Safety Review)**: Automatically generated reports must be scanned to ensure no unmasked client IDs or causal algorithm claims are published.
