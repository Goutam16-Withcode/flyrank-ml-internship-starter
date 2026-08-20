# Capstone Report — Content Refresh Prioritization

- **Author:** FlyRank ML Intern
- **Lane:** Content Refresh Prioritization (SEO Decay Prevention)
- **Repo:** `flyrank-ml-internship-starter`
- **Date:** 2026-08-20

---

## 0. Abstract

We investigate machine learning models for detecting organic search ranking decay across 30,000 anonymized web pages from the FlyRank search dataset. Using supervised binary classification with client-grouped holdout validation, we compare hand-written heuristic rules against a Random Forest model. Our primary evaluation metric, Precision@50, measures the proportion of truly decaying pages within the top 50 prioritized recommendations. The Random Forest model achieves a **Precision@50 of 0.740**, representing a **3.08x lift** over the transparent rule baseline (0.240 Precision@50). The output is an automated, ranked content update queue that enables editorial teams to maximize traffic recovery per editor-hour.

---

## 1. Problem framing

Organic search traffic decays over time due to content staleness, search engine algorithm updates, and emerging competitor pages. Editorial teams operate under capacity constraints (reviewing ~50 pages/week). 
- **Unit of Analysis**: Anonymized URL / Page ID (`page_id`).
- **Output**: Ranked refresh queue with continuous prediction score $P(\text{is\_declining}) \in [0, 1]$ and primary reason codes.
- **Action**: Editorial teams review top-ranked pages to perform content updates and technical SEO refreshes.
- **Cost of Wrong Call**: False positives waste editorial time ($150–$300 per review); false negatives lead to compounding loss of organic search traffic and revenue.

---

## 2. Data safety

- **Dataset**: `data/raw/content_refresh_anonymized.csv` (30,000 pseudonymized rows × 44 columns).
- **Prohibited Features**: Label-derived fields `trend_direction` and `trend_pct` were strictly excluded from feature sets to prevent feature leakage.
- **Pseudonymous IDs**: `page_id` and `client_id` were used exclusively for group splitting and candidate matching, never as numeric features.
- **Public Safety**: No client names, raw URLs, domains, or unmasked credentials exist within `work/`. All findings are stated in observed, measured, and decision-support terminology.

---

## 3. Baseline

The transparent hand-rule baseline flags pages based on four heuristic conditions:
$$\text{Baseline Score} = 0.35 \cdot \mathbb{I}(\text{days\_since\_last\_update} > 180) + 0.25 \cdot \mathbb{I}(\text{impressions\_90d} > 100) + 0.20 \cdot \mathbb{I}(\text{ctr} < 0.02) + 0.20 \cdot \mathbb{I}(\text{avg\_position} > 15)$$

On the evaluation set, the hand-rule baseline achieves **Precision@50 = 0.240**, providing a transparent benchmark to measure machine learning performance.

---

## 4. Model / analysis

We evaluated Logistic Regression, Decision Tree, and Random Forest models. The Random Forest classifier ($N_{\text{trees}} = 100$, $\text{max\_depth} = 10$) was selected for its non-linear feature interaction modeling and robustness against outliers.

- **Target Definition**: Binary target $y = 1$ if $\text{trend\_direction} == \text{'down'}$, else $y = 0$. Base rate in dataset: **34.5%**.
- **Features Included**: 18 numeric features (log-transformed counts: `log_impressions_90d`, `log_clicks_90d`, `log_sessions_90d`, `days_since_last_update`, `content_age_days`, `ctr`, `avg_position`, `engagement_rate`, `scroll_rate`) and 7 categorical features.

---

## 5. Evaluation

- **Split Strategy**: GroupShuffleSplit by `client_id` (80% train / 20% test holdout). This ensures zero client overlap between training and testing sets, reflecting real-world deployment on unseen client domains.
- **Performance**:
  - Base Rate (Declining Pages): **0.345**
  - Hand-Rule Baseline Precision@50: **0.240**
  - Random Forest Precision@50: **0.740** (**3.08x lift over baseline**)

---

## 6. Interpretation

Feature importance analysis reveals that search decay is primarily driven by:
1. `days_since_last_update` (21.4% importance): Content staleness is the single strongest indicator of search performance decay.
2. `ctr` (18.3% importance): Declining click-through rate indicates SERP position loss or snippet irrelevance.
3. `avg_position` (15.2% importance): Drop in average ranking positions directly precedes traffic loss.

---

## 7. Recommendation

We recommend deploying the Random Forest ranked queue into FlyRank's weekly editorial workflow:
1. **Urgent Refresh (Top 50 Pages)**: Prioritize for immediate editorial update; expected precision ~74%.
2. **Monitor (Ranks 51–500)**: Schedule technical audit if ranking position drops further.
3. **Retain (Remaining Pages)**: Re-evaluate during quarterly review.

---

## 8. Reproducibility

- **Environment**: Python 3.10 with `scikit-learn`, `pandas`, `numpy`.
- **Random Seed**: Fixed `random_state = 42`.
- **Re-run Pipeline**:
  ```bash
  $env:PYTHONUTF8=1; python scripts/run_all.py
  ```

---

## 9. Acknowledgments & data credit

Built on the FlyRank ML Internship dataset hosted by [FlyRank](https://flyrank.ai).
