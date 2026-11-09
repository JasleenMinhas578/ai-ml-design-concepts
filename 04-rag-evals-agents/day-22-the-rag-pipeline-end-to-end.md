# Day 22: The RAG Pipeline End to End

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Reverse Linked List (Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Copy values to a list and rebuild backwards: O(n) extra space.

**Best approach:** Three pointers: prev = None, curr = head. Save next, point curr.next to prev, move both forward. Return prev.

```python
def reverseList(head):
    prev, curr = None, head
    while curr:
        nxt = curr.next
        curr.next = prev
        prev, curr = curr, nxt
    return prev
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A university builds a bot over 2,000 course PDFs. Students ask 'What's the late policy for CS101?' The system retrieves the matching syllabus chunks, and the LLM answers with the policy and a link to the page it came from.

### What to understand

**Why RAG**  
LLMs don't know your private or recent data and can hallucinate. RAG grounds answers in retrieved documents.

**Ingestion**  
Load documents (PDF, HTML, Docs), parse text and tables, clean, and attach metadata (source, date, permissions).

**Chunk and embed**  
Split into chunks, convert each to a vector with an embedding model.

**Index**  
Store vectors and metadata in a vector database.

**Retrieve**  
Embed the user's query, find the top-k most similar chunks.

**Augment and generate**  
Put chunks into the prompt with instructions to answer only from them and cite sources.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Walk me through a RAG system.**  
Ingest → chunk → embed → index offline; at query time embed the query → retrieve top-k → build prompt → generate with citations.

**Q2. Why not put all documents in the context window?**  
Cost, latency, context limits, and models lose focus in very long contexts.

**Q3. What's the difference between offline and online parts of RAG?**  
Offline: ingestion and indexing. Online: retrieval and generation per query.

**Q4. What can go wrong in RAG?**  
Bad parsing, poor chunks, wrong retrieval, missing context, or the model ignoring the context.

---

## Part 3: Out-loud check (15 min)

> Draw the full RAG pipeline from memory.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Offline: ingest → chunk → embed → index
- Online: embed query → retrieve → prompt → generate
- Grounding + citations reduce hallucination
- Keep metadata (source, date, access)
- Failures can be at any stage
