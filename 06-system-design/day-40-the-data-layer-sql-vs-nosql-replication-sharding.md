# Day 40: The Data Layer: SQL vs NoSQL, Replication, Sharding

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Combination Sum (Backtracking, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Generate every combination and filter: exponential with lots of waste.

**Best approach:** Backtrack with a start index (to avoid duplicates); reuse the same number allowed; stop when the sum exceeds the target.

```python
def combinationSum(candidates, target):
    res = []
    def bt(start, path, total):
        if total == target:
            res.append(path[:]); return
        if total > target:
            return
        for i in range(start, len(candidates)):
            path.append(candidates[i])
            bt(i, path, total + candidates[i])
            path.pop()
    bt(0, [], 0)
    return res
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A ride-sharing app keeps payments in Postgres (strict consistency), driver locations in a fast key-value store updated every 2 seconds, and read replicas for trip history. When users reach 50 million, trips are sharded by city.

### What to understand

**SQL (relational)**  
Tables, schemas, joins, ACID transactions. Best for structured data and consistency (payments, orders).

**NoSQL**  
Key-value (Redis), document (MongoDB), wide-column (Cassandra), graph (Neo4j). Flexible schema, scales horizontally.

**Indexing**  
Speeds reads on queried columns; costs writes and storage.

**Replication**  
Copies of data on several machines: leader handles writes, followers serve reads. Improves availability and read speed.

**Sharding**  
Split data across machines by a key (user_id, region). Choose keys that spread load evenly to avoid hot shards.

**CAP theorem**  
During a network partition you choose consistency or availability. Banks lean to consistency; social feeds lean to availability.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. When would you choose NoSQL?**  
Huge scale, flexible schema, simple key-based access, high write rates.

**Q2. Replication vs sharding?**  
Replication copies the same data; sharding splits different data across machines.

**Q3. Explain CAP with an example.**  
If the network splits, a bank refuses writes to stay consistent; a social app keeps accepting posts and syncs later.

**Q4. What's a hot shard?**  
One shard getting much more traffic, e.g. a celebrity's data; fix with better keys or splitting.

---

## Part 3: Out-loud check (15 min)

> Explain SQL vs NoSQL choice and CAP with examples.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- SQL = ACID + joins
- NoSQL = scale + flexible
- Replicas for reads + availability
- Shard by an even key
- CAP: pick C or A during partition
