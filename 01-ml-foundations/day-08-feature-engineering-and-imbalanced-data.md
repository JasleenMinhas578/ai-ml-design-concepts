# Day 8: Feature Engineering and Imbalanced Data

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Subarray Sum Equals K (Prefix sum + hash map, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Check every subarray sum: O(n²).

**Best approach:** Keep a running sum and a dict of how often each prefix sum has appeared (start with {0: 1}). At each step add `count[sum - k]` to the answer.

```python
def subarraySum(nums, k):
    count = {0: 1}
    total = ans = 0
    for n in nums:
        total += n
        ans += count.get(total - k, 0)
        count[total] = count.get(total, 0) + 1
    return ans
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

An e-commerce site predicts returns. City has 5,000 values, price ranges widely, and 8% of rows miss 'age'. They target-encode city out-of-fold, scale price for the logistic model, add an 'age_missing' flag, and use class weights since only 5% are returns.

### What to understand

**Scaling**  
Standardisation (mean 0, std 1) or min-max. Needed for distance-based and gradient-based models, not for trees.

**Encoding categoricals**  
One-hot for few categories; target encoding or embeddings for many (watch for leakage with target encoding).

**Missing values**  
Drop, impute (mean/median/most frequent), or add a 'was missing' flag. Fit the imputer on train only.

**Class imbalance**  
Use class weights, resampling (undersample majority, oversample minority, SMOTE), or tune the threshold.

**Feature creation**  
Ratios, date parts, aggregations (e.g. avg spend over 30 days), text length. Domain knowledge wins here.

**Pipelines**  
Wrap preprocessing and model in one pipeline so CV applies preprocessing correctly and avoids leakage.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Name three ways to handle class imbalance.**  
Class weights, resampling/SMOTE, and threshold tuning with the right metric (PR-AUC).

**Q2. Do tree models need feature scaling?**  
No; splits depend on order, not scale.

**Q3. What's the risk with target encoding?**  
Leakage; compute it with out-of-fold means and smoothing.

**Q4. How do you handle a categorical feature with 10,000 values?**  
Target/frequency encoding, hashing, grouping rare values into 'other', or learned embeddings.

---

## Part 3: Out-loud check (15 min)

> Name 3 ways to handle imbalanced data and when each fits.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Scale for distance/gradient models, not trees
- One-hot (few) vs target encoding (many)
- Impute + missing flag
- Imbalance: weights, SMOTE, threshold
- Pipelines prevent leakage
