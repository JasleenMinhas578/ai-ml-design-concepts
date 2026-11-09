# Day 42: Design: URL Shortener

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Climbing Stairs (DP, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Plain recursion: f(n) = f(n−1) + f(n−2), exponential time.

**Best approach:** It's Fibonacci: keep only the last two values. O(n) time, O(1) space.

```python
def climbStairs(n):
    a, b = 1, 1
    for _ in range(n):
        a, b = b, a + b
    return a
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Design bit.ly: 100M new links a month and 10 billion redirects a month (100:1 read-heavy). Redirects must take under 50 ms.

### What to understand

**Requirements**  
Create short URL, redirect, optional custom alias and expiry, analytics. Very read-heavy.

**Estimates**  
~40 writes/s and ~4,000 reads/s average; ~500 bytes per link → ~600 GB over 10 years.

**Short ID generation**  
Base62 of an auto-increment ID or a distributed ID generator (7 chars = 3.5 trillion). Avoid random collisions or check uniqueness.

**Storage**  
Key-value or SQL table: short_id → long_url, created_at, expiry, user_id.

**Redirect path**  
Cache popular short_ids in Redis; 301 (permanent, browser caches) vs 302 (temporary, better for analytics).

**Analytics**  
Push click events to a queue and process asynchronously, so redirects stay fast.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How do you generate unique short codes?**  
Base62-encode a unique counter or ID from a distributed generator; or hash + collision check.

**Q2. 301 vs 302?**  
301 is cached by browsers (less load, fewer analytics); 302 hits your server every time.

**Q3. How do you scale reads?**  
Cache hot links, read replicas, CDN/edge.

**Q4. How do you collect click analytics without slowing redirects?**  
Send events to a queue and process them in the background.

---

## Part 3: Out-loud check (15 min)

> Design a URL shortener on paper in 30 minutes.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Read-heavy (100:1)
- Base62 of unique ID
- Cache hot links
- 301 vs 302
- Analytics via queue
