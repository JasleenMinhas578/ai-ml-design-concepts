# Day 31: LLM Latency

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Validate Binary Search Tree (Tree, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Only check each node against its children: wrong, because the rule applies to the whole subtree.

**Best approach:** Pass down allowed (low, high) bounds; each node must satisfy low < val < high. Or check that in-order traversal is strictly increasing.

```python
def isValidBST(root, low=float('-inf'), high=float('inf')):
    if not root:
        return True
    if not (low < root.val < high):
        return False
    return (isValidBST(root.left, low, root.val) and
            isValidBST(root.right, root.val, high))
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A chatbot takes 9 seconds to reply and users leave. Streaming makes the first words appear in 0.5 s, a smaller model handles simple questions, and caching repeated questions makes 30% of replies instant.

### What to understand

**TTFT vs total latency**  
Time to first token is what users feel; total time depends on output length.

**Throughput**  
Tokens or requests per second the system can handle; batching raises it.

**Streaming**  
Send tokens as they're generated so the user sees progress immediately.

**Smaller/faster models and routing**  
Send easy requests to small models, hard ones to large models.

**Quantisation**  
Store weights in INT8/INT4 instead of FP16: less memory, faster, small quality loss.

**Caching**  
Exact cache for repeated prompts, semantic cache for similar questions, prompt caching for long shared prefixes.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How would you reduce LLM latency?**  
Stream, shorten prompts and outputs, use smaller models or routing, cache, and run independent calls in parallel.

**Q2. What is TTFT?**  
Time until the first token appears; key for perceived speed.

**Q3. What is quantisation's trade-off?**  
Faster and smaller, with some accuracy loss.

**Q4. What is a semantic cache?**  
Reuse answers for queries whose embeddings are very similar.

---

## Part 3: Out-loud check (15 min)

> Give 3 ways to cut latency and explain the trade-offs.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- TTFT = felt speed
- Stream responses
- Route easy → small model
- Quantise INT8/INT4
- Cache: exact, semantic, prompt
