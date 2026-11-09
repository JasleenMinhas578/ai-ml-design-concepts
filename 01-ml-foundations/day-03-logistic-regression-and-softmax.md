# Day 3: Logistic Regression and Softmax

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Valid Anagram (Hash map, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Sort both strings and compare: O(n log n).

**Best approach:** Count letters of `s` in a dict, subtract counts for `t`; all counts must end at zero. Or compare `Counter(s) == Counter(t)`.

```python
def isAnagram(s, t):
    if len(s) != len(t):
        return False
    count = {}
    for a, b in zip(s, t):
        count[a] = count.get(a, 0) + 1
        count[b] = count.get(b, 0) - 1
    return all(v == 0 for v in count.values())
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A hospital screens patients for a disease. The model outputs probabilities; at 0.5 it misses 30% of sick patients. Lowering the threshold to 0.2 catches 95%, with more follow-up tests. Same model, different threshold, based on the cost of a miss.

### What to understand

**Logistic regression**  
A linear model whose output goes through a sigmoid, giving a probability between 0 and 1. Used for binary classification.

**Sigmoid**  
σ(z) = 1 / (1 + e^−z). Squashes any number into (0, 1).

**Log loss (binary cross-entropy)**  
Penalises confident wrong predictions heavily. It's convex for logistic regression, so gradient descent finds the global minimum.

**Decision boundary and threshold**  
Default threshold is 0.5, but you can move it to trade precision for recall.

**Softmax**  
Generalises sigmoid to many classes: turns a vector of scores into probabilities that sum to 1. Paired with categorical cross-entropy.

**Odds and coefficients**  
Each coefficient changes the log-odds. e^w is the multiplicative change in odds per unit of the feature.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Why not use MSE for logistic regression?**  
With a sigmoid, MSE is non-convex and gives weak gradients; log loss is convex and gives stronger signals.

**Q2. Is logistic regression a regression or classification model?**  
Classification. It regresses the log-odds, then thresholds the probability.

**Q3. How do you handle multi-class with logistic regression?**  
Softmax (multinomial) or one-vs-rest.

**Q4. When would you lower the threshold below 0.5?**  
When missing positives is costly, e.g. disease screening; you accept more false positives for higher recall.

---

## Part 3: Out-loud check (15 min)

> Why is log loss used instead of MSE for classification?

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Sigmoid → probability (0,1)
- Log loss: punishes confident mistakes
- Threshold is a business choice
- Softmax for multi-class
- Coefficient → change in log-odds
