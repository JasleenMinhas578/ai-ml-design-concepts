# Day 19: Decoding and Inference Basics

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Binary Search (Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Linear scan: O(n).

**Best approach:** lo, hi pointers; mid = (lo + hi) // 2; move lo or hi based on comparison. Watch the loop condition and off-by-one errors.

```python
def search(nums, target):
    lo, hi = 0, len(nums) - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        if nums[mid] == target:
            return mid
        if nums[mid] < target:
            lo = mid + 1
        else:
            hi = mid - 1
    return -1
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

An invoice-extraction service gets different totals on the same invoice across runs. Setting temperature to 0 and requiring JSON output makes results consistent. The marketing slogan generator keeps temperature 0.9 for variety.

### What to understand

**Greedy decoding**  
Always pick the most likely next token. Deterministic but can be repetitive.

**Beam search**  
Keep the top-k partial sequences. Good for translation; less used for chat.

**Temperature**  
Divides logits before softmax. Low (0–0.3) = focused and repeatable; high (0.8+) = more creative and random.

**Top-k and top-p (nucleus)**  
Top-k samples from the k most likely tokens. Top-p samples from the smallest set whose probability adds to p.

**KV cache**  
Stores past keys and values so each new token doesn't recompute attention for the whole sequence. Big speed win, costs memory.

**Prefill vs decode**  
Prefill processes the prompt in parallel; decode generates tokens one at a time.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. What does temperature do?**  
Controls randomness; lower is more deterministic, higher is more diverse.

**Q2. Top-p vs top-k?**  
Top-p adapts the candidate set to the model's confidence; top-k always uses a fixed count.

**Q3. What settings for a data-extraction task?**  
Temperature near 0 for consistent, factual output.

**Q4. What is the KV cache?**  
Cached attention keys/values from earlier tokens to speed up generation.

---

## Part 3: Out-loud check (15 min)

> Explain temperature and top-p, and settings for extraction vs creative writing.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Greedy = top token each step
- Temperature: low = focused, high = creative
- Top-p = smallest set summing to p
- KV cache = reuse past attention
- Prefill parallel; decode one token at a time
