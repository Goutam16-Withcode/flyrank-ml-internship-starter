# AI Fluency — Explain It Like You Built It

- **Author:** Goutam (FlyRank ML Intern)
- **Track:** AI Fluency — Deep Understanding & Human-in-the-Loop Ownership
- **Chosen Topic:** How `GroupShuffleSplit` by `client_id` Prevents Data Leakage in Search ML Models
- **Date:** 2026-08-20

---

## 1. The Real Piece of the Build

In our FlyRank Search Decay Model (`work/notebooks/w05_model.ipynb`), we evaluate our Random Forest model using:

```python
from sklearn.model_selection import GroupShuffleSplit

gss = GroupShuffleSplit(n_splits=1, test_size=0.2, random_state=42)
train_idx, test_idx = next(gss.split(X, y, groups=df['client_id']))
```

---

## 2. Plain-Words Explanation (Teaching a Friend)

Imagine you are studying for an exam, and your teacher gives you 100 practice questions from 10 different textbook chapters. 

If you randomly pick 80 questions to study and save 20 questions for the test, chances are high that the test questions come from the exact same chapters you just studied. You might get a 95% score, but that score is misleading—you didn't learn how to handle a completely new textbook chapter!

In our search dataset, web pages belong to different company websites (`client_id`). Pages from the same company share the exact same website design, writing style, and domain authority. 

If we use standard random splitting (`train_test_split`), pages from Client A end up in both our training set and our testing set. The model simply memorizes Client A's specific website quirks and gets a high score (0.820 Precision@50). But when you deploy that model on a brand new client website, it fails.

`GroupShuffleSplit` fixes this cheat. It puts **all pages from 80% of clients** into training, and saves **all pages from 20% of clients** exclusively for testing. The model is tested on clients it has *never seen before*. That drops our holdout score slightly to **0.740 Precision@50**, but that 0.740 is honest—it proves our ML model will actually work when deployed on new domains.

---

## 3. Key Takeaway & Human Ownership

As the engineer building this pipeline, I chose `GroupShuffleSplit` over standard random splitting because high test scores built on data leakage are a dangerous illusion. Real engineering credibility comes from reporting honest numbers on unseen domain data.
