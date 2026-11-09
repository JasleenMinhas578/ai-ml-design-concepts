# Day 4: Bias, Variance and Regularisation

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Group Anagrams (Hash map, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Compare every pair of words for anagram-ness: O(n² · k).

**Best approach:** Use a dict where the key is the sorted word (or a 26-letter count tuple) and the value is the list of words. Return the dict's values.

```python
from collections import defaultdict

def groupAnagrams(strs):
    groups = defaultdict(list)
    for w in strs:
        groups[tuple(sorted(w))].append(w)
    return list(groups.values())
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A student's spam classifier hits 99% on training emails but 70% on new ones. It memorised specific sender addresses. Adding L2 regularisation, removing the sender-ID feature and collecting more data brings test accuracy to 92%.

### What to understand

**Bias**  
Error from overly simple assumptions. High bias = underfitting: bad on train and test.

**Variance**  
Error from sensitivity to training data. High variance = overfitting: great on train, poor on test.

**Learning curves**  
Plot train and validation error vs data size or epochs. Big gap = variance; both high = bias.

**L2 regularisation (Ridge)**  
Adds λ·Σw² to the loss. Shrinks weights smoothly; good when many features matter a little.

**L1 regularisation (Lasso)**  
Adds λ·Σ|w|. Pushes some weights to exactly zero, so it does feature selection.

**Other fixes**  
Overfitting: more data, simpler model, dropout, early stopping, augmentation. Underfitting: more features, bigger model, less regularisation.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How do you tell if a model is overfitting?**  
Training score much better than validation score; validation loss rises while training loss falls.

**Q2. L1 vs L2: when would you use each?**  
L1 when you want a sparse model or feature selection; L2 for general shrinkage and correlated features.

**Q3. Does more data fix high bias?**  
No. More data helps variance. High bias needs a more expressive model or better features.

**Q4. What is the bias-variance trade-off?**  
Making a model more flexible lowers bias but raises variance; you aim for the sweet spot with the lowest validation error.

---

## Part 3: Out-loud check (15 min)

> Look at a train/val curve and say: overfit, underfit, or good, and the fix.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- High bias = underfit (bad everywhere)
- High variance = overfit (train ≫ test)
- L1 → zeros (feature selection)
- L2 → small weights
- More data fixes variance, not bias
