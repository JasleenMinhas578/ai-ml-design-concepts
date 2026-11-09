# Day 15: Tokenisation and Embeddings

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Longest Repeating Character Replacement (Sliding window, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Try every window and check if it can be fixed: O(n²).

**Best approach:** Keep counts in the window and the max frequency. If window size − maxFreq > k, shrink from the left. Answer is the largest valid window.

```python
def characterReplacement(s, k):
    count, left, maxf, best = {}, 0, 0, 0
    for right, ch in enumerate(s):
        count[ch] = count.get(ch, 0) + 1
        maxf = max(maxf, count[ch])
        while (right - left + 1) - maxf > k:
            count[s[left]] -= 1
            left += 1
        best = max(best, right - left + 1)
    return best
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A legal-tech app searches contracts. Keyword search for 'terminate' misses clauses saying 'end the agreement'. Embedding search finds both because their vectors sit close together. A rare clause code like 'ZX-44' still needs keyword search.

### What to understand

**Tokenisation**  
Splitting text into tokens. Word-level has huge vocabularies; character-level gives long sequences; subword is the balance.

**BPE and WordPiece**  
Subword methods that merge frequent character pairs, so rare words become pieces ('unhappiness' → 'un', 'happi', 'ness').

**Tokens and cost**  
LLM limits and pricing are in tokens (~0.75 words each in English).

**Embeddings**  
Dense vectors where similar meanings sit close together. Learned from context.

**Static vs contextual embeddings**  
Word2Vec gives one vector per word; transformer embeddings change with context ('bank' of a river vs a bank account).

**Cosine similarity**  
Measures angle between vectors; the standard way to compare embeddings.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Why do LLMs use subword tokenisation?**  
Small vocabulary with no unknown words, and sequences stay reasonably short.

**Q2. Why do similar words get similar vectors?**  
Words used in similar contexts get pushed toward similar positions during training.

**Q3. Cosine similarity vs Euclidean distance?**  
Cosine ignores vector length and focuses on direction; common for text embeddings.

**Q4. How do sentence embeddings differ from word embeddings?**  
They represent the whole sentence's meaning, often by pooling token vectors or training with contrastive loss.

---

## Part 3: Out-loud check (15 min)

> Explain why similar meanings end up as nearby vectors.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Subword tokens (BPE): no unknown words
- ~0.75 words per token
- Embedding = meaning as a vector
- Contextual > static embeddings
- Compare with cosine similarity
