# Day 28: Hallucination and Guardrails

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Maximum Depth of Binary Tree (DFS, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Collect every root-to-leaf path and measure them: extra memory.

**Best approach:** Depth = 1 + max(depth(left), depth(right)). Or BFS counting levels.

```python
def maxDepth(root):
    if not root:
        return 0
    return 1 + max(maxDepth(root.left), maxDepth(root.right))
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A travel bot invents a refund policy that doesn't exist and a customer screenshots it. The fix: answer only from retrieved policy text, cite the source, and reply 'I don't have that information' when nothing relevant is found.

### What to understand

**Why LLMs hallucinate**  
They predict plausible text, not verified facts; gaps in knowledge or context get filled with fluent guesses.

**Grounding**  
Provide source text (RAG) and instruct the model to answer only from it.

**Citations**  
Require the source for each claim; makes answers checkable and reduces invention.

**Abstaining**  
Allow and encourage 'I don't know' when context is missing.

**Guardrails**  
Input checks (injection, PII, off-topic) and output checks (schema validation, banned content, fact checks against sources).

**Verification**  
A second pass or model checks claims against context before showing the answer.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Three ways to reduce hallucination?**  
RAG grounding with 'answer only from context', citations, and allowing the model to say it doesn't know.

**Q2. What are guardrails?**  
Checks around the model on inputs and outputs, like validation, filters and policy rules.

**Q3. Can lowering temperature remove hallucinations?**  
It reduces randomness, but the model can still be confidently wrong.

**Q4. How would you detect hallucinations in production?**  
Faithfulness checks against retrieved context, user feedback, and sampled human review.

---

## Part 3: Out-loud check (15 min)

> Name 3 ways to reduce hallucinations and how each works.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Hallucination = fluent guess
- Ground in context + cite
- Allow 'I don't know'
- Guardrails on input and output
- Low temperature ≠ truth
