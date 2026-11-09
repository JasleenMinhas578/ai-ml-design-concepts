# Day 18: How LLMs Are Trained

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Daily Temperatures (Monotonic stack, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** For each day scan forward for a warmer one: O(n²).

**Best approach:** Keep a stack of indices with decreasing temperatures. When a warmer day arrives, pop and record the distance. O(n).

```python
def dailyTemperatures(temps):
    res = [0] * len(temps)
    stack = []  # indices
    for i, t in enumerate(temps):
        while stack and temps[stack[-1]] < t:
            j = stack.pop()
            res[j] = i - j
        stack.append(i)
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A base model asked 'How do I reset my password?' just continues with more questions, like a forum page. After SFT on Q&A pairs it answers. After DPO on preference pairs, its answers become clearer, safer and more concise.

### What to understand

**Pretraining**  
Next-token prediction on huge text corpora; the model learns language and world knowledge.

**Supervised fine-tuning (SFT)**  
Train on curated instruction-response pairs so the model follows instructions.

**RLHF**  
Humans rank responses, a reward model learns preferences, then the LLM is optimised (e.g. PPO) to score higher.

**DPO**  
Learns directly from preference pairs without a separate reward model; simpler and more stable than RLHF.

**Context window**  
Max tokens the model can see at once (prompt + output).

**Scaling laws and emergent behaviour**  
Loss improves predictably with more data, parameters and compute.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. SFT vs RLHF?**  
SFT teaches the format of good answers from examples; RLHF tunes toward what humans prefer when there's no single right answer.

**Q2. What is DPO and why use it?**  
Preference optimisation without a reward model or RL loop; cheaper and more stable.

**Q3. Why can't an LLM know recent events?**  
Its knowledge is frozen at the training cutoff; RAG or tools supply fresh information.

**Q4. What is a context window?**  
The maximum number of tokens the model can attend to in one call.

---

## Part 3: Out-loud check (15 min)

> Explain the pretraining → SFT → RLHF/DPO pipeline.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Pretrain = next-token on huge text
- SFT = learn to follow instructions
- RLHF = reward model + RL
- DPO = preferences, no reward model
- Knowledge frozen at cutoff
