# Day 44: ML Design: Recommendation System

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Coin Change (DP, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Try every combination recursively: exponential.

**Best approach:** dp[a] = fewest coins for amount a. dp[0] = 0; dp[a] = min(dp[a − coin] + 1) over coins. O(amount × coins).

```python
def coinChange(coins, amount):
    dp = [0] + [float('inf')] * amount
    for a in range(1, amount + 1):
        for c in coins:
            if c <= a:
                dp[a] = min(dp[a], dp[a - c] + 1)
    return dp[amount] if dp[amount] != float('inf') else -1
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Design 'recommended videos' for a platform with 10M videos and 50M users. You can't score 10M videos per request, so you narrow to 1,000 candidates, rank those, and show the top 20.

### What to understand

**Two-stage architecture**  
Candidate generation (fast, broad: 10M → ~1,000) then ranking (accurate, heavier: → top 20).

**Candidate generation**  
Collaborative filtering, two-tower embeddings with ANN search, trending and 'similar to watched'.

**Ranking**  
Gradient boosting or a neural net predicting click/watch time using user, item and context features.

**Features and feature store**  
User history, item stats, time of day; computed consistently for training and serving.

**Cold start**  
New users: popular items and onboarding questions. New items: content-based features.

**Metrics**  
Offline: recall@k, nDCG. Online: CTR, watch time, retention via A/B tests. Add diversity to avoid filter bubbles.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Why two stages?**  
Scoring millions of items with a heavy model per request is too slow.

**Q2. How do you handle cold start?**  
Popularity, onboarding preferences and content features.

**Q3. Offline vs online metrics?**  
Offline (nDCG) guides development; online (CTR, retention) via A/B tests decides launch.

**Q4. How would you run an A/B test?**  
Randomly split users, pick a primary metric, run for enough time and sample size, check significance and guardrail metrics.

---

## Part 3: Out-loud check (15 min)

> Design a recommender end to end in 35 minutes.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Candidates → ranking → re-rank
- Two-tower + ANN
- Feature store
- Cold start: popularity + content
- Offline nDCG; online A/B
