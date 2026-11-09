# Day 12: SQL Part 1: Core Queries

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Container With Most Water (Two pointers, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Try every pair of lines: O(n²).

**Best approach:** Pointers at both ends; area = min(height) × width. Move the pointer at the shorter line inward. O(n).

```python
def maxArea(height):
    l, r, best = 0, len(height) - 1, 0
    while l < r:
        best = max(best, min(height[l], height[r]) * (r - l))
        if height[l] < height[r]:
            l += 1
        else:
            r -= 1
    return best
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A marketing analyst needs customers who signed up last month but never bought. A LEFT JOIN from customers to orders with `WHERE o.id IS NULL` finds them in one query for a re-engagement email.

### What to understand

**SELECT, WHERE, ORDER BY, LIMIT**  
Pick columns, filter rows, sort, and cap results.

**Execution order**  
FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT. Explains why you can't use a SELECT alias in WHERE.

**Joins**  
INNER = matching rows only. LEFT = all left rows, NULLs where no match. FULL OUTER = everything. SELF JOIN = table with itself (e.g. employee and manager).

**GROUP BY and aggregates**  
COUNT, SUM, AVG, MIN, MAX per group.

**WHERE vs HAVING**  
WHERE filters rows before grouping; HAVING filters groups after aggregation.

**NULL handling**  
NULL ≠ NULL; use IS NULL. COUNT(col) skips NULLs; COALESCE gives a default.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Find customers who never ordered.**  
`SELECT c.* FROM customers c LEFT JOIN orders o ON c.id = o.customer_id WHERE o.id IS NULL;`

**Q2. WHERE vs HAVING?**  
WHERE filters rows before aggregation; HAVING filters aggregated groups.

**Q3. COUNT(*) vs COUNT(col)?**  
COUNT(*) counts all rows; COUNT(col) skips NULLs in that column.

**Q4. Find duplicate emails.**  
`SELECT email FROM users GROUP BY email HAVING COUNT(*) > 1;`

---

## Part 3: Out-loud check (15 min)

> Write a LEFT JOIN query to find users with no orders.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
- LEFT JOIN + IS NULL = 'never did X'
- WHERE filters rows; HAVING filters groups
- NULL needs IS NULL
- COUNT(col) skips NULLs
