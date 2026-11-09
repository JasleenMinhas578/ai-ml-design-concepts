# Day 20: Prompting vs RAG vs Fine-Tuning

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Search in Rotated Sorted Array (Binary search, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Linear scan: O(n).

**Best approach:** At each mid, one half is sorted. Check if the target lies in the sorted half; search there, otherwise search the other half.

```python
def search(nums, target):
    lo, hi = 0, len(nums) - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        if nums[mid] == target:
            return mid
        if nums[lo] <= nums[mid]:  # left half sorted
            if nums[lo] <= target < nums[mid]:
                hi = mid - 1
            else:
                lo = mid + 1
        else:  # right half sorted
            if nums[mid] < target <= nums[hi]:
                lo = mid + 1
            else:
                hi = mid - 1
    return -1
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

An HR team wants a bot answering policy questions. Policies change monthly, so they build RAG with citations. Later they fine-tune a small model with LoRA to match the company tone and cut cost, while still using RAG for facts.

### What to understand

**Prompting**  
Cheapest and fastest. Try first; good for format and behaviour.

**RAG**  
Add relevant external documents at query time. Best for fresh, private or frequently changing knowledge, with citations.

**Fine-tuning**  
Updates weights. Best for style, format, narrow tasks or domain language; not great for adding facts.

**LoRA**  
Freezes the base model and trains small low-rank matrices added to weights. Far fewer trainable parameters.

**QLoRA**  
LoRA on a 4-bit quantised base model, so large models fine-tune on one GPU.

**Decision rule**  
Prompt first → add RAG for knowledge → fine-tune for behaviour or cost at scale. They combine well.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Fine-tune or RAG for a company FAQ bot?**  
RAG: facts change, you need citations, and updating documents is cheaper than retraining.

**Q2. When is fine-tuning the right choice?**  
Consistent style/format, specialised tasks, or distilling to a smaller, cheaper model.

**Q3. What is LoRA and why is it efficient?**  
Trains small low-rank adapters instead of all weights, saving memory and time.

**Q4. Can fine-tuning reliably add new facts?**  
Not well; it tends to cause hallucinations. RAG is better for knowledge.

---

## Part 3: Out-loud check (15 min)

> Answer: fine-tune or RAG for a company FAQ bot, and why?

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Order: prompt → RAG → fine-tune
- RAG = knowledge + citations
- Fine-tune = style/format/task
- LoRA = small trainable adapters
- QLoRA = LoRA on 4-bit model
