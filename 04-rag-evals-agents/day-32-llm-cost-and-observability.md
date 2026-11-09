# Day 32: LLM Cost and Observability

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Lowest Common Ancestor of a BST (Tree, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Find both paths from the root and compare them: extra memory.

**Best approach:** Use BST order: if both values are smaller, go left; if both larger, go right; otherwise the current node is the answer.

```python
def lowestCommonAncestor(root, p, q):
    node = root
    while node:
        if p.val < node.val and q.val < node.val:
            node = node.left
        elif p.val > node.val and q.val > node.val:
            node = node.right
        else:
            return node
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A startup's LLM bill jumps from $2k to $20k a month. Tracing shows a 6,000-token system prompt sent every call and retries on every timeout. Prompt caching, trimming context and routing simple tasks to a small model cut the bill by 70%.

### What to understand

**Cost drivers**  
Input tokens + output tokens × price per model; output tokens usually cost more.

**Reduce tokens**  
Shorter prompts, fewer retrieved chunks, summarised history, capped output length.

**Prompt caching**  
Reuse long, unchanged prompt prefixes at a discount.

**Model routing and batching**  
Cheap model for simple tasks; batch APIs for non-urgent jobs.

**Observability**  
Trace each request: prompt, retrieved chunks, tool calls, tokens, latency, cost, errors (LangSmith, Langfuse, OpenTelemetry).

**Dashboards and alerts**  
Track cost per user/feature, p95 latency, error rate and quality scores.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Three ways to cut LLM cost?**  
Smaller models for easy tasks, fewer tokens (trim prompts and context), and caching.

**Q2. What would you log for an LLM app?**  
Inputs, outputs, retrieved docs, tool calls, tokens, latency, cost and user feedback, with PII handled carefully.

**Q3. Why trace multi-step agents?**  
To see which step failed or cost the most.

**Q4. What is p95 latency?**  
95% of requests are faster than this; shows the slow tail better than an average.

---

## Part 3: Out-loud check (15 min)

> Name 3 ways to cut LLM cost and what you'd monitor.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Cost = tokens × price
- Trim prompts and context
- Prompt caching + routing
- Trace every step
- Watch cost, p95, errors, quality
