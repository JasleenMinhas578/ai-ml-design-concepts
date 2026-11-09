# Day 47: AI Design: Customer-Support Agent

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Unique Paths (2D DP, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Recursion trying every path: exponential.

**Best approach:** Each cell's paths = paths from above + paths from the left. Keep one row: row[j] += row[j−1]. O(m × n).

```python
def uniquePaths(m, n):
    row = [1] * n
    for _ in range(1, m):
        for j in range(1, n):
            row[j] += row[j - 1]
    return row[-1]
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

An airline wants an agent that can check bookings, change flights and issue refunds. The agent can look up and suggest changes freely, but refunds over $200 need a human agent to approve.

### What to understand

**Tools**  
Read tools (lookup booking, check policy) and write tools (change flight, refund), each with strict schemas.

**Permissions and limits**  
Least privilege; write actions limited by amount and user identity; confirmations for risky steps.

**Grounding**  
Policies come from RAG, not the model's memory.

**Escalation**  
Hand off to a human when confidence is low, the customer is upset, or the action is high-risk, with a summary.

**Safety**  
Prompt-injection defences, PII handling, audit logs of every action.

**Evals**  
Scenario tests (simulated customers), task success rate, wrong-action rate, escalation rate, customer satisfaction.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How do you stop an agent taking unsafe actions?**  
Limited tools, server-side checks, approval for high-risk actions, and audit logs.

**Q2. When should it escalate to a human?**  
High risk, low confidence, repeated failure, or customer request.

**Q3. How do you evaluate an agent?**  
Scenario-based tests measuring task success and wrong actions, then live metrics.

**Q4. Why enforce limits in code, not just the prompt?**  
Prompts can be bypassed; code checks can't be talked around.

---

## Part 3: Out-loud check (15 min)

> Design the support agent and explain how you stop unsafe actions.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Read tools free; write tools limited
- Enforce rules in code
- Policies via RAG
- Escalate with a summary
- Scenario evals + audit logs
