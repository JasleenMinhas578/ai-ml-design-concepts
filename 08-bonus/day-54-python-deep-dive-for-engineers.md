# Day 54: BONUS: Python Deep Dive for Engineers

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Generate Parentheses (Backtracking, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Generate all 2^(2n) strings and filter valid ones.

**Best approach:** Backtrack: add '(' if open < n; add ')' if close < open.

```python
def generateParenthesis(n):
    res = []
    def bt(s, open_, close):
        if len(s) == 2 * n:
            res.append(s); return
        if open_ < n: bt(s + '(', open_ + 1, close)
        if close < open_: bt(s + ')', open_, close + 1)
    bt('', 0, 0)
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Your script calls an LLM API for 1,000 documents one at a time and takes 50 minutes. Using asyncio with a concurrency limit of 20 brings it to 3 minutes, because the time was spent waiting on the network, not computing.

### What to understand

**GIL**  
Only one thread runs Python bytecode at a time. Threads help with I/O-bound work; use multiprocessing for CPU-bound work.

**asyncio**  
Single-threaded concurrency for many I/O waits (API calls); use a semaphore to cap concurrency.

**OOP essentials**  
Classes, inheritance vs composition, dunder methods, @dataclass, @property.

**Decorators and context managers**  
Decorators wrap functions (logging, retries, caching); `with` handles setup and cleanup.

**Type hints and Pydantic**  
Make code clearer and catch bugs; Pydantic validates at runtime.

**Mutable default arguments**  
`def f(x=[])` shares the list across calls; use `None` instead.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Threads vs processes vs asyncio?**  
Threads/asyncio for I/O-bound waits; processes for CPU-heavy work because of the GIL.

**Q2. What is a decorator?**  
A function that wraps another to add behaviour, like retries or timing.

**Q3. Why is a mutable default argument dangerous?**  
It's created once and shared between calls.

**Q4. When use a dataclass?**  
For simple data containers, with auto-generated __init__ and __repr__.

---

## Part 3: Out-loud check (15 min)

> Explain the GIL and when you'd use asyncio vs multiprocessing.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- GIL: threads for I/O, processes for CPU
- asyncio + semaphore for API calls
- Decorators wrap behaviour
- Composition over inheritance
- No mutable defaults
