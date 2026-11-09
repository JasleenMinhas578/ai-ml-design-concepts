# Day 24: Vector Databases and Similarity Search

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Linked List Cycle (Fast/slow pointers, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Store visited nodes in a set: O(n) space.

**Best approach:** Slow moves 1 step, fast moves 2. If they ever meet, there's a cycle; if fast hits None, there isn't.

```python
def hasCycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow is fast:
            return True
    return False
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A startup's FAISS flat index takes 2 seconds per query at 5 million chunks. Switching to an HNSW index brings it to 20 ms with 98% of the same results. They add a 'department' filter so users only see documents they're allowed to see.

### What to understand

**Vector database**  
Stores embeddings and finds nearest neighbours fast. Examples: FAISS (library), Chroma, pgvector (Postgres), Pinecone, Weaviate, Qdrant.

**Similarity metrics**  
Cosine (direction), dot product (direction + length), Euclidean/L2 (distance). Use what the embedding model was trained with.

**Exact vs approximate search**  
Exact compares against every vector (slow at scale). ANN trades a little accuracy for big speed gains.

**HNSW**  
Graph-based ANN index: navigates layers of linked neighbours. Fast and accurate, but memory-heavy.

**IVF and PQ**  
IVF clusters vectors and searches only nearby clusters. Product quantisation compresses vectors to save memory.

**Metadata filtering**  
Filter by fields (department, date, permissions) before or during the vector search.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Why approximate nearest neighbour search?**  
Exact search is O(n) per query; ANN gives near-identical results much faster on millions of vectors.

**Q2. pgvector vs Pinecone?**  
pgvector: keep vectors in your existing Postgres. Pinecone: managed, scales easily, costs more.

**Q3. How does HNSW work at a high level?**  
A multi-layer graph; start at the top sparse layer, greedily move closer, drop down layers to refine.

**Q4. How do you enforce user permissions in RAG?**  
Store access metadata on chunks and filter on it at query time.

---

## Part 3: Out-loud check (15 min)

> Explain why approximate search is used, and what HNSW does.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Vector DB = nearest-neighbour search
- Cosine / dot / L2
- ANN: fast, slightly approximate
- HNSW = layered graph; IVF = clusters
- Filter by metadata for permissions
