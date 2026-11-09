# Day 6: Regression Metrics, Cross-Validation and Tuning

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Product of Array Except Self (Array, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** For each index multiply all other elements: O(n²). Division fails with zeros.

**Best approach:** Two passes: fill output with prefix products from the left, then multiply by suffix products from the right. No division, O(1) extra space.

```python
def productExceptSelf(nums):
    n = len(nums)
    res = [1] * n
    left = 1
    for i in range(n):
        res[i] = left
        left *= nums[i]
    right = 1
    for i in range(n - 1, -1, -1):
        res[i] *= right
        right *= nums[i]
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A retailer forecasts weekly sales. Random 5-fold CV gives a great RMSE, but the model fails next quarter because folds trained on future weeks. Switching to rolling time-series CV gives a worse but honest score that matches reality.

### What to understand

**MAE, MSE, RMSE**  
MAE = average absolute error (robust to outliers). RMSE = square root of MSE, in the target's units, punishes big errors.

**R²**  
Fraction of variance explained compared with predicting the mean. 1 is perfect; 0 equals the mean baseline.

**K-fold cross-validation**  
Split data into k folds; train on k−1, validate on 1, rotate, and average. Gives a more stable estimate.

**Stratified and time-series CV**  
Stratified keeps class ratios in each fold. Time-series CV always validates on later data (rolling window).

**Grid vs random search**  
Grid tries every combination (expensive). Random samples combinations and usually finds good values faster. Bayesian optimisation (Optuna) learns from past trials.

**Nested CV**  
Inner loop tunes, outer loop evaluates, so the tuning doesn't bias the score.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. RMSE vs MAE: which would you report?**  
RMSE when big errors are especially bad; MAE when you want robustness and easy interpretation.

**Q2. Why not do k-fold on time-series data?**  
Random folds let the model train on the future and test on the past.

**Q3. Why is random search often better than grid search?**  
Only a few hyperparameters usually matter; random search explores more distinct values of each.

**Q4. What does negative R² mean?**  
The model is worse than just predicting the mean.

---

## Part 3: Out-loud check (15 min)

> Choose a CV strategy for (a) imbalanced data and (b) sales over time.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- MAE robust; RMSE punishes big misses
- R² < 0 → worse than mean
- K-fold for stable estimates
- Stratified for imbalance; rolling for time
- Random search > grid search
