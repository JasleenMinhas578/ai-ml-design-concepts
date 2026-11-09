# Day 39: Scaling Basics: Load Balancing, Caching, CDN

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Subsets (Backtracking, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Iterate over all bitmasks from 0 to 2ⁿ − 1: works and is fine.

**Best approach:** Backtrack: at each index, choose to include or skip the element. Or start with [[]] and add each number to every existing subset.

```python
def subsets(nums):
    res = [[]]
    for n in nums:
        res += [s + [n] for s in res]
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A news site crashes during an election. Adding a load balancer across 10 stateless servers, a Redis cache for top stories (95% hit rate) and a CDN for images lets it handle 50× the traffic.

### What to understand

**Vertical vs horizontal scaling**  
Vertical = bigger machine (simple, has a limit). Horizontal = more machines (needs a load balancer, scales further).

**Load balancer**  
Spreads requests across servers (round robin, least connections) and removes unhealthy ones.

**Stateless services**  
Keep no user session in server memory, so any server can handle any request.

**Caching**  
Store hot data in memory (Redis). Patterns: cache-aside, write-through. Eviction: LRU. Expiry: TTL.

**Cache invalidation**  
Keeping the cache fresh is the hard part: TTLs, delete on write, versioned keys.

**CDN**  
Servers worldwide caching static files (images, JS, video) close to users.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Where would you put a cache?**  
In front of the database for hot reads; at the edge (CDN) for static assets; for LLMs, in front of expensive model calls.

**Q2. Why make services stateless?**  
Easy horizontal scaling and failover.

**Q3. What is cache-aside?**  
App checks cache; on a miss reads the DB and writes the result to cache.

**Q4. Vertical vs horizontal scaling?**  
Bigger machine vs more machines.

---

## Part 3: Out-loud check (15 min)

> Explain where you'd add a cache and how you keep it fresh.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Horizontal > vertical at scale
- Load balancer + health checks
- Stateless servers
- Redis cache-aside, TTL, LRU
- CDN for static content
