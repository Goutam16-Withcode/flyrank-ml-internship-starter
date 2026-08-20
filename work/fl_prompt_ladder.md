# AI Fluency — 5-Step Prompt Engineering Ladder

- **Author:** Goutam (FlyRank Intern)
- **Track:** AI Fluency — Systematic Prompt Engineering & Iterative Optimization
- **Date:** 2026-08-20

---

## 1. Weak Baseline Prompt (Run 0)

### Prompt
> *"Write a Python script to train an ML model for search data."*

### Output Excerpt
> ```python
> import pandas as pd
> from sklearn.linear_model import LogisticRegression
> df = pd.read_csv("data.csv")
> model = LogisticRegression()
> model.fit(df.drop("label", axis=1), df["label"])
> print("Model trained!")
> ```

---

## 2. The 5-Step Iterative Prompt Ladder

### Version 1 — Layer Added: Clear Task & Business Context
- **Prompt**: *"Write a Python script to train a machine learning model that predicts organic search ranking decay across a dataset of web pages."*
- **4 Notes**:
  - *What Changed*: Specified domain problem (predicting search ranking decay on web pages).
  - *Output Improvement*: The output switched from generic classification to generating `trend_direction` target definitions and feature selection (`impressions`, `ctr`).
  - *What Still Failed*: It used `train_test_split(test_size=0.2)` randomly, causing domain leakage across pages belonging to the same client domain.
  - *What to Try Next*: Add target persona and split requirements.

### Version 2 — Layer Added: Target Validation Design (Grouped Split)
- **Prompt**: *"Write a Python script to train an ML model predicting search decay. Use GroupShuffleSplit by client_id (80% train / 20% test) so pages from a client never appear in both train and test."*
- **4 Notes**:
  - *What Changed*: Added `GroupShuffleSplit(n_splits=1, test_size=0.2)` by `client_id`.
  - *Output Improvement*: The code correctly imported `GroupShuffleSplit` and held out ~20% of `client_id` values, preventing data contamination.
  - *What Still Failed / Didn't Help (Honest Catch)*: The model trained, but it used `accuracy_score` as the metric, which was misleading because precision at top-K ranks is what editorial workflows need. High accuracy was easily achieved by predicting the majority class.
  - *What to Try Next*: Specify output format and evaluation metric (`Precision@50`).

### Version 3 — Layer Added: Output Format & Specific Metric
- **Prompt**: *"Write a Python script to train a Random Forest model for search decay using GroupShuffleSplit by client_id. Evaluate the model using Precision@50 (precision among top 50 predicted scores) and output the results as a formatted markdown table comparing Random Forest against a simple rule baseline."*
- **4 Notes**:
  - *What Changed*: Specified `Precision@50` metric and markdown table output format.
  - *Output Improvement*: The script defined a custom `precision_at_k` function and printed a clean Markdown table showing baseline vs Random Forest scores.
  - *What Still Failed*: The feature set accidentally included `trend_pct`, causing target leakage (1.000 precision).
  - *What to Try Next*: Add strict negative constraints excluding target proxy variables.

### Version 4 — Layer Added: Negative Constraints (No Leakage Allowed)
- **Prompt**: *"Write a Python script to train a Random Forest model for search decay with GroupShuffleSplit by client_id and Precision@50 evaluation. CONSTRAINTS: Strictly exclude trend_direction and trend_pct from model features as they are label proxies."*
- **4 Notes**:
  - *What Changed*: Added explicit negative constraint prohibiting target proxies `trend_direction` and `trend_pct`.
  - *Output Improvement*: The output dropped target proxy columns from `X`, resulting in an honest 0.740 Precision@50 score.
  - *What Still Failed*: The code lacked docstrings, comments, and runtime error checks for null values.
  - *What to Try Next*: Add code quality criteria and self-verification checks.

### Version 5 — Layer Added: Code Quality & Verification Instructions
- **Prompt**: *"Write a production-grade Python script to train a Random Forest classifier for search decay. Use GroupShuffleSplit by client_id. Exclude label proxies (trend_direction, trend_pct). Evaluate Precision@50 vs baseline. QUALITY CRITERIA: Include fillna(0) for missing metrics, add clean logging prints, and verify feature importances."*
- **4 Notes**:
  - *What Changed*: Added explicit code robustness guidelines and logging instructions.
  - *Output Improvement*: Output produced self-contained, clean Python code with exception handling, `fillna(0)` safety, feature importances, and step-by-step stdout prints.
  - *What Still Failed*: None — code executed cleanly and produced the target output.
  - *What to Try Next*: Finalize as a reusable team prompt template.

---

## 3. Final Reusable Production Prompt

```text
Act as a Senior ML Engineer. Write a production-grade Python script to train and evaluate a search ranking decay prediction model on pandas DataFrame `df`.

Task Requirements:
1. Define binary target: `y = (df['trend_direction'] == 'down').astype(int)`
2. Split strategy: GroupShuffleSplit by `client_id` (80% train / 20% test holdout) to prevent client domain leakage.
3. Feature constraints: Strictly exclude `trend_direction` and `trend_pct` from model features (target proxies).
4. Models: Train a Random Forest Classifier (100 trees, max_depth=10) and compare against a hand-written baseline rule.
5. Evaluation: Compute Precision@50 (precision among top 50 ranked pages) on the test holdout.
6. Output: Print summary log and top 10 feature importances.
```
