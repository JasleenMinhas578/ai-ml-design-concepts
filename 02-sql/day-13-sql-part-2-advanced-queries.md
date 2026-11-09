# Day 13: SQL Part 2: Advanced Queries

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Best Time to Buy and Sell Stock (Sliding window, Easy)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** For each buy day check every later sell day: O(n²).

**Best approach:** Track the lowest price so far; at each day compute price − min and keep the max profit. O(n).

```python
def maxProfit(prices):
    lowest, best = float('inf'), 0
    for p in prices:
        lowest = min(lowest, p)
        best = max(best, p - lowest)
    return best
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A product manager asks for each month's top 3 customers by revenue and the month-over-month change. A CTE sums revenue, DENSE_RANK picks the top 3 per month, and LAG computes the change from last month.

### What to understand

**Subqueries**  
A query inside another, in WHERE, FROM or SELECT. Correlated subqueries run per row (can be slow).

**CTEs (WITH)**  
Named temporary results that make complex queries readable; recursive CTEs walk hierarchies.

**Window functions**  
Compute across related rows without collapsing them: `func() OVER (PARTITION BY ... ORDER BY ...)`.

**ROW_NUMBER, RANK, DENSE_RANK**  
Numbering within groups. RANK leaves gaps on ties; DENSE_RANK doesn't.

**LAG / LEAD and running totals**  
Compare with previous/next row (e.g. month-over-month change). `SUM() OVER (ORDER BY date)` gives a running total.

**Indexes**  
Speed up lookups and joins on a column (B-tree) but slow down writes. Use EXPLAIN to check the query plan.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Top 3 customers by revenue per month.**  
CTE with `SUM(amount)` grouped by month and customer, then `DENSE_RANK() OVER (PARTITION BY month ORDER BY revenue DESC)`, filter rank ≤ 3.

**Q2. Second-highest salary.**  
`SELECT MAX(salary) FROM emp WHERE salary < (SELECT MAX(salary) FROM emp);` or DENSE_RANK = 2.

**Q3. RANK vs DENSE_RANK?**  
Ties 1,1 → RANK gives next 3, DENSE_RANK gives next 2.

**Q4. When can an index hurt?**  
Write-heavy tables, low-selectivity columns, and extra storage.

---

## Part 3: Out-loud check (15 min)

> Write a 'top 3 per group' query using a window function.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- CTE = readable named step
- OVER (PARTITION BY ... ORDER BY ...)
- ROW_NUMBER / RANK / DENSE_RANK
- LAG/LEAD = previous/next row
- Index speeds reads, slows writes
