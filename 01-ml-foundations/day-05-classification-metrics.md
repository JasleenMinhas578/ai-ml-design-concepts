# Day 5: Classification Metrics

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Top K Frequent Elements (Hash map + heap, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Count, then sort all items by frequency: O(n log n).

**Best approach:** Count with a dict, then either use a min-heap of size k (O(n log k)) or bucket sort by frequency (O(n)).

```python
from collections import Counter
import heapq

def topKFrequent(nums, k):
    count = Counter(nums)
    return heapq.nlargest(k, count, key=count.get)
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A payments company has 0.1% fraud. A model saying 'never fraud' scores 99.9% accuracy and catches nothing. The team switches to PR-AUC, then sets a threshold where recall is 85% and precision is 40%, because reviewing a false alarm costs $2 and missing fraud costs $500.

### What to understand

**Confusion matrix**  
TP, FP, FN, TN. Every classification metric is built from these four numbers.

**Precision**  
TP / (TP + FP). Of what I flagged, how much was right? Matters when false alarms are costly (spam filter).

**Recall**  
TP / (TP + FN). Of all real positives, how many did I catch? Matters when misses are costly (fraud, cancer).

**F1 score**  
Harmonic mean of precision and recall. Useful when you need one number on imbalanced data.

**ROC-AUC vs PR-AUC**  
ROC-AUC measures ranking ability across thresholds. PR-AUC is more informative when positives are rare.

**Threshold tuning**  
Pick the threshold based on business cost, not 0.5 by default.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Which metric for fraud detection?**  
Recall (catch fraud) balanced with precision (don't block good customers); report PR-AUC since fraud is rare.

**Q2. Why is accuracy misleading on imbalanced data?**  
Predicting the majority class scores high while catching zero positives.

**Q3. What does ROC-AUC of 0.5 mean?**  
The model ranks no better than random.

**Q4. How would you choose a threshold?**  
Plot precision/recall vs threshold and choose based on the cost of false positives vs false negatives.

---

## Part 3: Out-loud check (15 min)

> Pick and justify the metric for fraud detection vs spam filtering.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Precision = TP/(TP+FP): trust my alarms
- Recall = TP/(TP+FN): catch them all
- F1 = balance of both
- Rare positives → PR-AUC
- Choose threshold by cost
