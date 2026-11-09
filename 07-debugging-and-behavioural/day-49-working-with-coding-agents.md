# Day 49: Working With Coding Agents

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Merge Intervals (Intervals, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Compare every pair of intervals repeatedly: O(n²).

**Best approach:** Sort by start. Walk through; if the current interval overlaps the last merged one, extend its end; otherwise add it.

```python
def merge(intervals):
    intervals.sort(key=lambda x: x[0])
    res = [intervals[0]]
    for start, end in intervals[1:]:
        if start <= res[-1][1]:
            res[-1][1] = max(res[-1][1], end)
        else:
            res.append([start, end])
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

You ask an agent to 'add caching'. It rewrites 12 files and breaks auth. Next time you give context (which endpoint, Redis already available), constraints (don't touch auth), ask for a plan first, review the diff, and run the tests.

### What to understand

**Give context**  
Relevant files, architecture, conventions, what already exists.

**Set constraints**  
What not to change, libraries to use, performance or style rules.

**Plan first**  
Ask for a plan and review it before any code is written.

**Small steps**  
One focused change at a time; easier to review and roll back.

**Review and verify**  
Read the diff, run tests, ask it to explain choices; never merge code you don't understand.

**Use it well**  
Great for boilerplate, tests, refactors and explaining unfamiliar code; you stay responsible for design and correctness.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How do you use AI coding tools in your work?**  
Give clear context and constraints, ask for a plan, work in small steps, review diffs and verify with tests.

**Q2. How do you know AI-generated code is correct?**  
Read it, run tests, add tests for edge cases, and check it against requirements.

**Q3. What are risks of AI coding tools?**  
Subtle bugs, security issues, outdated APIs, and code you can't maintain.

**Q4. When wouldn't you use an agent?**  
Security-critical logic you can't verify, or when you don't understand the problem yet.

---

## Part 3: Out-loud check (15 min)

> Describe your workflow for using coding agents responsibly.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Context + constraints
- Plan before code
- Small steps
- Review diff + run tests
- You own the result
