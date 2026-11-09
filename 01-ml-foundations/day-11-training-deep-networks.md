# Day 11: Training Deep Networks

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** 3Sum (Two pointers, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Three nested loops: O(n³).

**Best approach:** Sort. For each index i, use two pointers on the rest to find pairs summing to −nums[i]. Skip duplicates. O(n²).

```python
def threeSum(nums):
    nums.sort()
    res = []
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i-1]:
            continue
        l, r = i + 1, len(nums) - 1
        while l < r:
            s = nums[i] + nums[l] + nums[r]
            if s < 0: l += 1
            elif s > 0: r -= 1
            else:
                res.append([nums[i], nums[l], nums[r]])
                l += 1
                while l < r and nums[l] == nums[l-1]:
                    l += 1
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

An image model's loss jumps around wildly in the first few hundred steps. Adding LR warmup plus cosine decay, switching to AdamW and adding dropout 0.1 stabilises it. Early stopping halts training at epoch 18 before validation loss rises.

### What to understand

**SGD with momentum**  
Keeps a running average of gradients so updates move smoothly and faster.

**Adam**  
Combines momentum with per-parameter adaptive learning rates. Strong default; AdamW adds proper weight decay.

**Learning-rate schedules**  
Warmup then decay (cosine, step). Warmup avoids early instability, especially in transformers.

**Weight initialisation**  
Xavier/He init keep activations at a sensible scale so training starts well.

**Batch norm vs layer norm**  
Batch norm normalises across the batch (CNNs). Layer norm normalises across features per example (transformers).

**Dropout and early stopping**  
Dropout randomly zeros neurons during training to prevent co-dependence. Early stopping ends training when validation loss stops improving.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. What does dropout do and is it used at inference?**  
Randomly drops neurons in training as regularisation; it's turned off at inference.

**Q2. Why is Adam a common default?**  
Adaptive step sizes per parameter make it work well with little tuning.

**Q3. Why do transformers use layer norm instead of batch norm?**  
It doesn't depend on batch size and works well with variable-length sequences.

**Q4. Your loss isn't decreasing. What do you check?**  
Learning rate, data/labels, loss function, gradients (NaN/zero), and whether you can overfit a tiny batch.

---

## Part 3: Out-loud check (15 min)

> Say what dropout, Adam and LR warmup each do.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Adam/AdamW = safe default
- Warmup + decay schedule
- Batch norm (CNN) vs layer norm (transformers)
- Dropout off at inference
- Debug: overfit one tiny batch first
