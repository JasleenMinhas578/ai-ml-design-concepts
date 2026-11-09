# Day 7: Decision Trees, Random Forests and Boosting

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Longest Consecutive Sequence (Hash set, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Sort and scan for runs: O(n log n).

**Best approach:** Put all numbers in a set. Only start counting from numbers where `n-1` is not in the set, then extend upward. O(n).

```python
def longestConsecutive(nums):
    s = set(nums)
    best = 0
    for n in s:
        if n - 1 not in s:
            length = 1
            while n + length in s:
                length += 1
            best = max(best, length)
    return best
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

An insurer predicts claim costs from 40 tabular features. A single decision tree overfits; a random forest is stable; XGBoost wins with the best validation score. SHAP values then explain each customer's prediction to regulators.

### What to understand

**Decision tree**  
Splits data with if/else questions to make groups purer. Easy to explain, but overfits easily.

**Gini and entropy**  
Impurity measures used to pick the best split; the split that reduces impurity most wins.

**Bagging and random forest**  
Train many trees on bootstrap samples with random feature subsets, then average. Reduces variance.

**Boosting**  
Train trees one after another, each fixing the errors of the previous ones. Reduces bias.

**XGBoost / LightGBM**  
Fast gradient-boosting libraries with regularisation; often the best choice for tabular data.

**Feature importance**  
Split-based importance can be biased; SHAP values give more reliable per-prediction explanations.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Bagging vs boosting?**  
Bagging: parallel, independent models, lowers variance. Boosting: sequential, each corrects the last, lowers bias.

**Q2. Why do random forests choose random features at each split?**  
To make trees less correlated, so averaging reduces variance more.

**Q3. When would you use XGBoost over a neural network?**  
Structured/tabular data, smaller datasets, need for speed and interpretability.

**Q4. How do you stop a single tree overfitting?**  
Limit max depth, set minimum samples per leaf, or prune.

---

## Part 3: Out-loud check (15 min)

> Explain bagging vs boosting in plain English with one example each.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Tree = if/else splits by impurity
- Bagging = parallel, lowers variance
- Boosting = sequential, lowers bias
- Tabular data → try XGBoost/LightGBM
- SHAP for explanations
