# Day 27: LLM Evals Part 2: Evaluating RAG

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Invert Binary Tree (Tree, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** There isn't really a slower version; the main mistake is forgetting the base case.

**Best approach:** Recursively swap left and right children at every node. O(n) time.

```python
def invertTree(root):
    if not root:
        return None
    root.left, root.right = invertTree(root.right), invertTree(root.left)
    return root
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A RAG bot gives wrong answers. Evaluating separately shows recall@5 is 0.95 (retrieval finds the right chunk) but faithfulness is 0.6 (the model ignores it). The fix is the prompt and generation, not the vector database.

### What to understand

**Evaluate retrieval and generation separately**  
So you know which half is broken.

**Recall@k**  
How often the correct chunk appears in the top k results.

**MRR / nDCG**  
Reward putting the right chunk near the top, not just somewhere in the list.

**Faithfulness (groundedness)**  
Is every claim in the answer supported by the retrieved context?

**Answer relevance and context precision**  
Does the answer address the question? How much retrieved context was actually useful?

**Tools and regression tests**  
RAGAS, DeepEval, TruLens, LangSmith. Run the eval suite in CI so changes can't silently break quality.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How do you know your RAG system is working well?**  
Measure retrieval (recall@k, MRR) and generation (faithfulness, relevance) on a golden set, plus user feedback in production.

**Q2. Answers are wrong but retrieval looks good. What now?**  
Check faithfulness: prompt clarity, context order, too much context, or the model overriding the context.

**Q3. What is faithfulness?**  
Whether the answer's claims are supported by the retrieved context.

**Q4. How do you prevent regressions?**  
Run evals automatically in CI on every prompt, model or chunking change.

---

## Part 3: Out-loud check (15 min)

> Explain how to tell if a bad answer is a retrieval or generation problem.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Split: retrieval vs generation
- Retrieval: recall@k, MRR
- Generation: faithfulness, relevance
- RAGAS / DeepEval / LangSmith
- Evals in CI
