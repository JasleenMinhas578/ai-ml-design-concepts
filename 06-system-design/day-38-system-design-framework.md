# Day 38: System Design Framework

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Rotting Oranges (Multi-source BFS, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Simulate minute by minute, scanning the whole grid each time: O((rows·cols)²).

**Best approach:** Put all rotten oranges in a queue at once; BFS level by level, counting minutes. If fresh oranges remain, return −1.

```python
from collections import deque

def orangesRotting(grid):
    rows, cols = len(grid), len(grid[0])
    q, fresh = deque(), 0
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 2: q.append((r, c))
            elif grid[r][c] == 1: fresh += 1
    minutes = 0
    while q and fresh:
        for _ in range(len(q)):
            r, c = q.popleft()
            for dr, dc in ((1,0),(-1,0),(0,1),(0,-1)):
                nr, nc = r + dr, c + dc
                if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 1:
                    grid[nr][nc] = 2
                    fresh -= 1
                    q.append((nr, nc))
        minutes += 1
    return minutes if fresh == 0 else -1
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Asked to 'design Instagram', a candidate jumps straight into databases and runs out of time. Another spends 5 minutes on requirements ('feed, upload, follow; 10M daily users; feed under 200 ms'), and the rest of the interview flows from that.

### What to understand

**1. Requirements**  
Functional (what it does) and non-functional (scale, latency, availability, consistency). Ask questions.

**2. Estimates**  
Users, requests per second, storage, bandwidth. Rough numbers are fine.

**3. API and data model**  
Main endpoints and the key tables/entities.

**4. High-level design**  
Boxes and arrows: clients, load balancer, services, databases, cache, queues.

**5. Deep dive**  
Pick 1–2 hard parts (scaling the feed, hot keys) and go deep.

**6. Trade-offs and bottlenecks**  
Say what you chose and what you gave up; mention monitoring and failure handling.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. How do you start a system design interview?**  
Clarify requirements and scale before drawing anything.

**Q2. Functional vs non-functional requirements?**  
Functional = features. Non-functional = performance, scale, reliability, security.

**Q3. How do you estimate QPS?**  
Daily active users × actions per user ÷ 86,400 seconds; multiply by 2–3 for peak.

**Q4. What do interviewers look for?**  
Structured thinking, clear communication and reasoned trade-offs, not one 'right' answer.

---

## Part 3: Out-loud check (15 min)

> Recite the 6 steps and do a quick QPS estimate.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Requirements first (ask!)
- Estimate: QPS, storage
- API + data model
- Boxes and arrows
- Deep dive + trade-offs
