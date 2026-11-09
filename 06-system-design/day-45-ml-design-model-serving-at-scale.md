# Day 45: ML Design: Model Serving at Scale

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Longest Increasing Subsequence (DP, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** dp[i] = 1 + max(dp[j]) for j < i with nums[j] < nums[i]: O(n²). Good to explain first.

**Best approach:** Patience sorting: keep a list `tails`; binary-search where each number fits and replace. Length of `tails` is the answer. O(n log n).

```python
import bisect

def lengthOfLIS(nums):
    tails = []
    for n in nums:
        i = bisect.bisect_left(tails, n)
        if i == len(tails):
            tails.append(n)
        else:
            tails[i] = n
    return len(tails)
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A bank scores fraud on every card swipe within 100 ms (real-time), but scores credit-limit increases for all customers overnight (batch). A new model version first gets 5% of traffic (canary) before full rollout.

### What to understand

**Batch inference**  
Score large datasets on a schedule; cheap and simple, results can be stale.

**Real-time inference**  
Score per request behind an API with tight latency limits.

**Streaming inference**  
Score events as they arrive from Kafka, near real-time.

**Autoscaling and GPUs**  
Scale replicas on load; GPUs for large models, with batching to keep them busy (vLLM, Triton).

**Safe rollout**  
Shadow mode (new model runs silently), canary, A/B test, fast rollback.

**Monitoring**  
Latency, errors, prediction distribution, drift and business metrics.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Batch vs real-time inference?**  
Batch for non-urgent bulk scoring; real-time when each request needs a fresh answer.

**Q2. What is shadow deployment?**  
The new model receives real traffic but its outputs aren't used, so you can compare safely.

**Q3. How do you serve a large LLM efficiently?**  
GPU batching, quantisation, KV-cache optimisation, autoscaling (e.g. vLLM).

**Q4. How do you roll back a bad model?**  
Keep the previous version in the registry and switch traffic back.

---

## Part 3: Out-loud check (15 min)

> Explain batch vs real-time serving and a safe rollout plan.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Batch = scheduled bulk
- Real-time = per request, low latency
- Shadow → canary → full
- GPU batching, quantisation
- Monitor latency, drift, business KPIs
