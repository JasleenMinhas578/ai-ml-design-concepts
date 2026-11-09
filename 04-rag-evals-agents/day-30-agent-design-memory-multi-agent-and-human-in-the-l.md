# Day 30: Agent Design: Memory, Multi-Agent and Human-in-the-Loop

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Binary Tree Level Order Traversal (BFS, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** DFS while tracking depth, then group by depth: works but less natural.

**Best approach:** BFS with a queue; for each level, process exactly `len(queue)` nodes and collect their values.

```python
from collections import deque

def levelOrder(root):
    if not root:
        return []
    res, q = [], deque([root])
    while q:
        level = []
        for _ in range(len(q)):
            node = q.popleft()
            level.append(node.val)
            if node.left: q.append(node.left)
            if node.right: q.append(node.right)
        res.append(level)
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A recruiting assistant uses one agent to search candidates, one to draft outreach, and pauses for a recruiter's approval before sending any email. It remembers each recruiter's preferred tone across sessions.

### What to understand

**Short-term memory**  
The conversation history inside the context window; summarise or trim when it gets long.

**Long-term memory**  
Facts stored outside the model (vector DB or database) and retrieved when relevant.

**Multi-agent systems**  
Specialised agents (researcher, writer, reviewer) with an orchestrator. Useful for separate skills, but adds cost, latency and debugging difficulty.

**LangGraph**  
Models agent workflows as a graph with state, branches, loops and checkpoints.

**Human-in-the-loop**  
Pause for approval before risky or irreversible actions (sending email, payments, deletions).

**MCP**  
Model Context Protocol: a standard way to connect models to tools and data sources.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. When would you use multiple agents?**  
When tasks need clearly different skills or tools, or can run in parallel; otherwise one agent is simpler.

**Q2. How do you give an agent memory?**  
Short-term via context (with summarisation), long-term via a store retrieved by relevance.

**Q3. Where would you add human approval?**  
Before irreversible, costly or external actions.

**Q4. What's hard about multi-agent systems?**  
Coordination, error propagation, cost, and debugging.

---

## Part 3: Out-loud check (15 min)

> Explain when to use multi-agent vs single agent, and where humans approve.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Short-term = context; long-term = store
- Multi-agent only when needed
- LangGraph = stateful graph
- Human approval for risky actions
- MCP = standard tool connections
