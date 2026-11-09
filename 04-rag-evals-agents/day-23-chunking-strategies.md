# Day 23: Chunking Strategies

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Merge Two Sorted Lists (Linked list, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Put all nodes into a list, sort, and rebuild: O(n log n).

**Best approach:** Use a dummy head; repeatedly attach the smaller node and advance. Attach whatever list remains.

```python
def mergeTwoLists(l1, l2):
    dummy = tail = ListNode()
    while l1 and l2:
        if l1.val <= l2.val:
            tail.next, l1 = l1, l1.next
        else:
            tail.next, l2 = l2, l2.next
        tail = tail.next
    tail.next = l1 or l2
    return dummy.next
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A RAG bot over employee handbooks splits every 100 tokens with no overlap. A question about parental leave gets a chunk with half the policy. Switching to heading-based chunks of ~500 tokens with 15% overlap fixes the answers.

### What to understand

**Fixed-size chunking**  
Split every N tokens. Simple, but can cut sentences or ideas in half.

**Recursive chunking**  
Try to split on paragraphs, then sentences, then words, until under the size limit. Good default.

**Semantic chunking**  
Split where embedding similarity between sentences drops, so each chunk is one topic.

**Structure-aware chunking**  
Use document structure: headings, sections, tables, code blocks.

**Size and overlap**  
Typical 200–800 tokens with 10–20% overlap. Small = precise but lacks context; large = context but noisy and diluted.

**Metadata and parent-child**  
Store title, section, page and date. Parent-child: retrieve small chunks but send the larger parent section to the LLM.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. What goes wrong with chunks that are too big?**  
Embeddings get diluted, retrieval gets less precise, and you waste tokens.

**Q2. What goes wrong with chunks that are too small?**  
They lose context, so answers become incomplete.

**Q3. Why use overlap?**  
So information at chunk boundaries isn't lost.

**Q4. How would you chunk a technical manual with tables?**  
Structure-aware: split by headings, keep tables whole, add section titles as metadata.

---

## Part 3: Out-loud check (15 min)

> Explain the chunk-size trade-off and your default choice.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Default: recursive, 200–800 tokens
- Overlap 10–20%
- Too big = noisy; too small = no context
- Respect structure (headings, tables)
- Parent-child: search small, send big
