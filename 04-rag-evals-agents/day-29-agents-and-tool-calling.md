# Day 29: Agents and Tool Calling

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Same Tree (Tree, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Serialise both trees to strings and compare: works but uses extra memory.

**Best approach:** Recursively: both empty → True; one empty or values differ → False; else compare left and right subtrees.

```python
def isSameTree(p, q):
    if not p and not q:
        return True
    if not p or not q or p.val != q.val:
        return False
    return isSameTree(p.left, q.left) and isSameTree(p.right, q.right)
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A user asks 'What's the weather in Toronto, and should I bike to work?' The agent calls a weather tool, reads 'heavy rain', then answers. Without tools it would have guessed.

### What to understand

**Agent**  
An LLM in a loop that decides which actions to take, uses tools, sees results and continues until the goal is done.

**Tool calling**  
You describe tools with a name, description and JSON schema; the model outputs a structured call; your code runs it and returns the result.

**ReAct loop**  
Reason → Act (tool call) → Observe (result) → repeat.

**Planning**  
Break a goal into steps first, then execute, re-planning if something fails.

**Stop conditions**  
Max steps, max cost, timeouts and a clear 'done' check to avoid endless loops.

**Tool error handling**  
Return clear error messages to the model, retry with backoff, and fall back safely.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How does an agent decide which tool to call?**  
The model reads tool names, descriptions and schemas, and picks the one that best matches the current step; good descriptions matter.

**Q2. Agent vs workflow?**  
A workflow follows fixed steps in code; an agent decides its own steps. Use workflows when the path is predictable.

**Q3. How do you stop an agent looping forever?**  
Step and cost limits, timeouts, and loop detection.

**Q4. A tool keeps failing. How should the agent handle it?**  
Return a clear error, retry a limited number of times, then try another approach or escalate.

---

## Part 3: Out-loud check (15 min)

> Explain the ReAct loop and how tool calling works.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Agent = LLM + tools + loop
- Tool = name + description + schema
- Reason → Act → Observe
- Limits: steps, cost, time
- Prefer workflows when path is fixed
