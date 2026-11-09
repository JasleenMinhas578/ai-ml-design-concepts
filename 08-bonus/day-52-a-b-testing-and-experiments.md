# Day 52: BONUS: A/B Testing and Experiments

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Koko Eating Bananas (Binary search on answer, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Try every speed from 1 upward: O(max × n).

**Best approach:** Binary search the speed k between 1 and max(piles); check hours = Σ ceil(p / k) ≤ h.

```python
import math

def minEatingSpeed(piles, h):
    lo, hi = 1, max(piles)
    while lo < hi:
        k = (lo + hi) // 2
        if sum(math.ceil(p / k) for p in piles) <= h:
            hi = k
        else:
            lo = k + 1
    return lo
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A new AI search ranking raises clicks by 3% after two days. Checking properly: the test needed two weeks for enough sample size, and the gain shrinks to 0.5% (a novelty effect). It's still significant, and latency (a guardrail metric) didn't get worse.

### What to understand

**Setup**  
Random split into control and treatment; one primary metric decided in advance.

**Sample size and power**  
Decide how many users you need before starting, based on the smallest effect worth detecting.

**Significance**  
p < 0.05 or a confidence interval excluding zero; don't stop early when it 'looks good' (peeking).

**Guardrail metrics**  
Make sure you didn't break something else (latency, revenue, complaints).

**Pitfalls**  
Novelty effects, too-short tests, testing many metrics at once, users seeing both versions.

**LLM features**  
Combine offline evals with online A/B tests on user outcomes (resolution rate, satisfaction).

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How would you A/B test a new model?**  
Randomise users, choose a primary metric and guardrails, compute sample size, run full weeks, then check significance.

**Q2. What is peeking and why is it bad?**  
Checking repeatedly and stopping when significant inflates false positives.

**Q3. What is a guardrail metric?**  
A metric that must not get worse, such as latency or cost.

**Q4. Result is significant but tiny. Ship it?**  
Consider practical value vs cost and complexity, not just the p-value.

---

## Part 3: Out-loud check (15 min)

> Design an A/B test for a new chatbot model.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Randomise; one primary metric
- Sample size before starting
- No peeking
- Guardrails
- Watch novelty effects
