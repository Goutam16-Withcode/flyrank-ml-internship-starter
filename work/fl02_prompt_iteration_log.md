# FL-02 — Interactive Prompt Engineering & Cross-Model Audit

- **Author:** Goutam (FlyRank Intern)
- **Track:** AI Fluency — FL-02 Interactive Prompt Optimization & Cross-Model Benchmark
- **Target Task (from FL-01)**: Exploratory Data Analysis (EDA) & Signal Profiling on Search Data
- **Date:** 2026-08-20

---

## 1. The Naive Baseline Prompt (Run 0)

### Prompt
> *"Write a pandas python code for data analysis."*

### Observed Output
Generates a generic 5-line script creating dummy DataFrame data with `df.describe()`. Completely lacks domain context or dataset metrics.

---

## 2. The 5-Step Technique Iteration Ladder (Runs 1 to 5)

### Iteration 1 — Technique: Role Assignment
- **Prompt**: *"Act as a Senior Data Scientist. Write a pandas python code for data analysis."*
- **Observed Output Difference**: The code now includes proper function structures, type hinting, and basic logging statements (`print("Data loaded")`), moving beyond simple script fragments.

### Iteration 2 — Technique: Context & Motivation
- **Prompt**: *"Act as a Senior Data Scientist. Write a pandas script to perform Exploratory Data Analysis on a 30,000-row search intelligence dataset (`content_refresh_anonymized.csv`) to identify signals associated with search ranking decay."*
- **Observed Output Difference**: Output switched from generic dummy data to referencing specific search columns (`impressions_90d`, `clicks_90d`, `days_since_last_update`, `avg_position`) and calculating Pearson correlations against a binary target.

### Iteration 3 — Technique: Output Structure Specification
- **Prompt**: *"Act as a Senior Data Scientist performing EDA on a search decay dataset. Structure your output into two parts: 1) A clean Python function returning summary metrics, 2) A Markdown table summarizing top 5 correlated features."*
- **Observed Output Difference**: Output separated code logic from human-readable text, producing a clean GitHub Flavored Markdown summary table alongside modular Python code.

### Iteration 4 — Technique: Few-Shot Examples
- **Prompt**: *"Act as a Senior Data Scientist. Perform EDA on search decay data. Format summary outputs as shown in this example: `| Feature | Correlation | Verdict |` `| days_since_last_update | +0.284 | Strong Decay Signal |`"*
- **Observed Output Difference**: Output strictly adhered to the requested column schema and added automated qualitative verdicts (`Strong Decay Signal`, `Weak Signal`) for each feature correlation.

### Iteration 5 — Technique: Step Decomposition (Chain-of-Thought)
- **Prompt**: *"Act as a Senior Data Scientist. Perform EDA on search decay data (`content_refresh_anonymized.csv`) following these exact steps: Step 1: Load data and fill missing numeric values with 0. Step 2: Compute target label `is_declining_label = (trend_direction == 'down')`. Step 3: Compute Pearson correlations for all numeric features. Step 4: Output Markdown summary table. Step 5: Generate seaborn bar chart visualization code."*
- **Observed Output Difference**: Output produced a step-by-step pipeline script matching all 5 execution stages cleanly without omitting data imputation or visualization setup.

---

## 3. Cross-Model Comparison (Claude vs ChatGPT)

We executed the final Iteration 5 prompt on both **Claude 3.5 Sonnet** and **ChatGPT (GPT-4o)**:

| Evaluation Axis | Claude 3.5 Sonnet | ChatGPT (GPT-4o) | Key Observation |
|---|---|---|---|
| **Code Tone & Style** | Concise, modular, uses type hints and vectorization. | Explanatory, includes verbose comments before every line. | Claude output was cleaner for direct copy-pasting into notebooks. |
| **Data Safety & Edge Cases** | Added `fillna(0)` and explicit `np.isfinite` bounds checking. | Used basic `.fillna(df.mean())` which introduced subtle target leakage. | Claude handled missing metric imputation more safely. |
| **Markdown Table Format** | Exact GFM table format matching requested few-shot example. | Added extra text headers and bullet points around the table. | Claude strictly adhered to structural constraints. |
| **Failure Points** | Occasional truncation on extremely long seaborn styling options. | Defaulted to deprecated pandas `.append()` syntax on older prompts. | ChatGPT required explicit `pd.concat` instruction. |

---

## 4. Final Reusable Prompt Template

```text
Act as a Senior Data Scientist specializing in Search Intelligence. Perform Exploratory Data Analysis on dataset `data/raw/content_refresh_anonymized.csv`.

Execution Steps:
1. Data Loading: Load CSV and impute missing numeric values with 0 (`df.fillna(0)`).
2. Target Definition: Compute binary label `is_declining_label = (df['trend_direction'] == 'down').astype(int)`.
3. Signal Audit: Calculate Pearson correlation between numeric features and `is_declining_label`.
4. Table Summary: Output a Markdown table listing Top 5 features: `| Feature | Correlation | Signal Strength |`.
5. Visualization: Generate standalone matplotlib/seaborn code to save a bar chart of top correlations to `outputs/charts/signal_correlations.png`.
```
