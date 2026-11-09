# Day 25: Improving Retrieval

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Remove Nth Node From End of List (Linked list, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Count the length first, then remove node (length − n): two passes.

**Best approach:** Dummy head; move fast pointer n steps ahead, then move both until fast reaches the end; slow.next is the node to remove.

```python
def removeNthFromEnd(head, n):
    dummy = ListNode(0, head)
    fast = slow = dummy
    for _ in range(n + 1):
        fast = fast.next
    while fast:
        fast, slow = fast.next, slow.next
    slow.next = slow.next.next
    return dummy.next
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Users ask an IT bot about error 'ERR-5021', but vector search returns generic error pages. Adding BM25 in a hybrid search finds the exact code, and a cross-encoder reranker moves the best chunk to position 1.

### What to understand

**BM25 (keyword search)**  
Classic ranking by term frequency. Great for exact terms, IDs, names and codes that embeddings miss.

**Hybrid search**  
Combine keyword and vector results; usually beats either alone.

**Reciprocal Rank Fusion (RRF)**  
Merges ranked lists by summing 1 / (k + rank) for each document.

**Reranking**  
A cross-encoder scores each (query, chunk) pair together; more accurate than embeddings. Retrieve top-50, rerank to top-5.

**Query rewriting**  
Use an LLM to clarify, expand or split the query; multi-query retrieval searches several versions.

**HyDE**  
Generate a hypothetical answer, embed it, and search with that; helps when queries are short or vague.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Your RAG retrieves irrelevant chunks. What do you try?**  
Check chunking, add hybrid search, add a reranker, rewrite queries, use metadata filters, try a better embedding model.

**Q2. Bi-encoder vs cross-encoder?**  
Bi-encoder embeds query and document separately (fast, for retrieval). Cross-encoder reads them together (accurate, for reranking).

**Q3. When does keyword search beat vector search?**  
Exact product codes, names, acronyms and rare terms.

**Q4. Why not rerank all documents?**  
Cross-encoders are slow; rerank only a small candidate set.

---

## Part 3: Out-loud check (15 min)

> Name 3 ways to fix bad retrieval and explain each.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Hybrid = BM25 + vectors
- RRF merges ranked lists
- Retrieve 50 → rerank to 5
- Rewrite vague queries
- HyDE: search with a fake answer
