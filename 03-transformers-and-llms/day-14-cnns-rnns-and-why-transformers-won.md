# Day 14: CNNs, RNNs and Why Transformers Won

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Longest Substring Without Repeating Characters (Sliding window, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Check every substring for repeats: O(n³).

**Best approach:** Move a right pointer; store each character's last index in a dict. If a repeat is inside the window, jump the left pointer past it. Track max length.

```python
def lengthOfLongestSubstring(s):
    last, left, best = {}, 0, 0
    for right, ch in enumerate(s):
        if ch in last and last[ch] >= left:
            left = last[ch] + 1
        last[ch] = right
        best = max(best, right - left + 1)
    return best
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A support team's LSTM ticket classifier struggles with long tickets where the key detail comes early, and training takes 10 hours. A fine-tuned transformer reads the whole ticket at once, trains in 2 hours and is 8 points more accurate.

### What to understand

**CNN**  
Convolution filters slide over images to detect local patterns (edges → shapes → objects). Weight sharing makes them efficient.

**Pooling**  
Downsamples feature maps, adding some translation invariance.

**RNN**  
Processes a sequence one step at a time with a hidden state carrying memory.

**LSTM / GRU**  
RNNs with gates that decide what to remember or forget, easing vanishing gradients.

**RNN limitations**  
Sequential (can't parallelise), struggles with long-range dependencies, slow to train.

**Why transformers won**  
Attention connects any two positions directly and processes all tokens in parallel, so they scale to huge data and GPUs.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Name two limitations of RNNs.**  
No parallelism across time steps, and difficulty with long-range dependencies.

**Q2. Why are CNNs good for images?**  
Local patterns plus weight sharing and some translation invariance.

**Q3. What problem do LSTMs solve?**  
Vanishing gradients over long sequences, via gating.

**Q4. Why do transformers train faster on GPUs?**  
All tokens are processed at once with matrix multiplications, instead of step by step.

---

## Part 3: Out-loud check (15 min)

> Explain 2 RNN limits and how transformers fix them.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- CNN = local filters + weight sharing
- RNN = step by step with memory
- LSTM gates help long memory
- RNNs: no parallelism, weak long-range
- Transformers: parallel + direct attention
