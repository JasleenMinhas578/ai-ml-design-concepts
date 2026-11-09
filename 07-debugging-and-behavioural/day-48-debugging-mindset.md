# Day 48: Debugging Mindset

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Maximum Subarray (Kadane, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Check every subarray: O(n²).

**Best approach:** Kadane: at each number, either extend the current subarray or start fresh: cur = max(n, cur + n). Track the best.

```python
def maxSubArray(nums):
    cur = best = nums[0]
    for n in nums[1:]:
        cur = max(n, cur + n)
        best = max(best, cur)
    return best
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Your RAG bot says the refund window is 14 days, but the policy says 30. You reproduce it with the same question, check retrieved chunks (an old 2023 policy ranks first), confirm the hypothesis by filtering to the latest version, then fix ingestion to drop outdated documents and add a test.

### What to understand

**1. Reproduce**  
Get a reliable failing case: same input, same config.

**2. Isolate**  
Narrow down the component: data, retrieval, prompt, model, code, infrastructure. Use logs and traces.

**3. Hypothesise and test**  
Form one theory, change one thing, check the result.

**4. Fix and verify**  
Fix the root cause, not the symptom; confirm it's fixed and nothing else broke.

**5. Prevent**  
Add a test or eval case so the bug can't come back.

**ML-specific checks**  
Loss not decreasing: LR, labels, data pipeline, overfit one batch. Great offline but bad online: leakage or drift. RAG wrong: retrieval vs generation.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Your RAG bot gives wrong answers. What do you check first?**  
Look at the retrieved chunks for that query: right chunks → generation problem; wrong chunks → retrieval/chunking/data problem.

**Q2. Training loss isn't decreasing. Steps?**  
Check data and labels, lower the LR, check the loss function and gradients, and try to overfit a tiny batch.

**Q3. Model is great offline but bad in production. Why?**  
Leakage, training/serving feature mismatch, or drift.

**Q4. API latency spiked. How do you investigate?**  
Check traces to find the slow step, recent deploys, traffic, and external dependencies.

---

## Part 3: Out-loud check (15 min)

> Narrate a debugging session out loud using the 5 steps.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Reproduce → isolate → hypothesise → fix → prevent
- Change one thing at a time
- RAG: check retrieved chunks first
- Training: overfit a tiny batch
- Every bug → a test
