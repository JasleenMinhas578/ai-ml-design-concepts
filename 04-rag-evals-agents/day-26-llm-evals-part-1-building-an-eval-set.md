# Day 26: LLM Evals Part 1: Building an Eval Set

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** LRU Cache (Hash map + doubly linked list, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Store items in a list and move them on access: O(n) per operation.

**Best approach:** A dict gives O(1) lookup; an ordered structure tracks recency. In Python, `OrderedDict` with `move_to_end` does both. In interviews, be ready to explain the dict + doubly linked list version.

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.cap = capacity
        self.cache = OrderedDict()
    def get(self, key):
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)
        return self.cache[key]
    def put(self, key, value):
        self.cache[key] = value
        self.cache.move_to_end(key)
        if len(self.cache) > self.cap:
            self.cache.popitem(last=False)
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A team changes their support-bot prompt and it 'feels better'. A week later, refund questions are answered wrongly. With a 150-question golden set, they would have seen the refund category drop from 92% to 71% before shipping.

### What to understand

**Why evals**  
LLM output varies and 'looks fine' isn't evidence. Evals turn quality into numbers you can compare across prompts, models and versions.

**Golden dataset**  
50–500 real questions with expected answers or criteria, covering common cases, edge cases and known failures.

**Reference-based metrics**  
Exact match, F1 on tokens, BLEU/ROUGE. Cheap, but they miss correct answers phrased differently.

**LLM-as-judge**  
A strong model grades outputs against a rubric (correct? complete? follows format?). Check it against human labels; watch for bias toward long answers and its own style.

**Human review**  
Gold standard for nuanced quality; use it to build and calibrate the dataset and judge.

**Offline vs online evals**  
Offline: test set before release. Online: user feedback, thumbs up/down, A/B tests and monitoring in production.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How would you evaluate an LLM feature?**  
Build a golden set from real queries, define a rubric, score with automatic checks plus LLM-as-judge validated on human labels, then track it on every change.

**Q2. Problems with LLM-as-judge?**  
Position and length bias, self-preference, inconsistency. Use clear rubrics, pairwise comparisons, and calibrate with humans.

**Q3. Why not just use BLEU?**  
It measures word overlap, not correctness; a correct paraphrase can score low.

**Q4. How big should an eval set be?**  
Start with ~50–100 good examples; grow it with every production failure.

---

## Part 3: Out-loud check (15 min)

> Describe how you'd build and run an eval set for a chatbot.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Golden set = real questions + expected answers
- Rubric → LLM-as-judge → check with humans
- BLEU/ROUGE miss paraphrases
- Offline before release, online after
- Every bug becomes a new test case
