# Day 41: Async Systems: Queues, Retries and Rate Limiting

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Word Search (Backtracking, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** None simpler that works; the key is marking cells visited.

**Best approach:** DFS from each cell matching the first letter; mark the cell visited, explore 4 directions, then unmark (backtrack).

```python
def exist(board, word):
    rows, cols = len(board), len(board[0])
    def dfs(r, c, i):
        if i == len(word):
            return True
        if r < 0 or c < 0 or r >= rows or c >= cols or board[r][c] != word[i]:
            return False
        tmp, board[r][c] = board[r][c], '#'
        found = any(dfs(r+dr, c+dc, i+1) for dr, dc in ((1,0),(-1,0),(0,1),(0,-1)))
        board[r][c] = tmp
        return found
    return any(dfs(r, c, 0) for r in range(rows) for c in range(cols))
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Users upload 500-page PDFs to a RAG app and the request times out. The API now puts a job on a queue and returns 'processing'; workers parse and embed in the background, retry failures, and notify the user when done.

### What to understand

**Message queues**  
Kafka, SQS, RabbitMQ. Producers add jobs; consumers process them later. Decouples services and absorbs spikes.

**Pub/sub**  
One event, many subscribers (e.g. 'order placed' → email, analytics, inventory).

**Workers**  
Background processes pulling jobs; scale them with the queue length.

**Retries and dead-letter queues**  
Retry with exponential backoff; after N failures, move to a dead-letter queue for inspection.

**Idempotency**  
Doing the same operation twice has the same effect as once; use idempotency keys so retries don't double-charge.

**Rate limiting**  
Protect services: token bucket (refill tokens at a fixed rate) or sliding window. Return 429 when exceeded.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Why use a queue?**  
Decouple services, handle spikes, and run slow work in the background.

**Q2. What is idempotency and why does it matter?**  
Safe retries; e.g. a payment with the same key is processed only once.

**Q3. Design a simple rate limiter.**  
Token bucket per user in Redis: each request takes a token; tokens refill at a fixed rate; empty → 429.

**Q4. What is a dead-letter queue?**  
Where messages go after repeated failures, so they don't block the queue.

---

## Part 3: Out-loud check (15 min)

> Explain why a queue, and design a token-bucket rate limiter.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Queue = decouple + absorb spikes
- Pub/sub = one event, many listeners
- Retry with backoff → DLQ
- Idempotency keys
- Token bucket → 429
