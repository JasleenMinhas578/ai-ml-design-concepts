# Day 9: Unsupervised Learning: K-Means and PCA

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Valid Sudoku (Hash set, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Check each row, column and box separately with lists: 3 passes.

**Best approach:** One pass over the grid with sets for each row, column and 3×3 box (box index = (r//3, c//3)). Any repeat means invalid.

```python
def isValidSudoku(board):
    rows, cols, boxes = set(), set(), set()
    for r in range(9):
        for c in range(9):
            v = board[r][c]
            if v == '.':
                continue
            keys = ((r, v), (c, v), (r // 3, c // 3, v))
            if keys[0] in rows or keys[1] in cols or keys[2] in boxes:
                return False
            rows.add(keys[0]); cols.add(keys[1]); boxes.add(keys[2])
    return True
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A gym chain clusters members by visit frequency, class types and spend. K-means with k=4 finds groups like 'weekend casuals' and 'daily lifters', used for targeted offers. PCA reduces 30 survey questions to 5 components for a quick 2D plot.

### What to understand

**K-means**  
Pick k centroids, assign points to the nearest one, move centroids to the mean, repeat until stable.

**Choosing k**  
Elbow method (inertia vs k) or silhouette score.

**K-means limitations**  
Assumes round, similar-sized clusters; sensitive to scale and initialisation (use k-means++).

**PCA**  
Finds new axes (principal components) that capture the most variance; keep the top few to reduce dimensions.

**Explained variance**  
How much of the data's spread each component keeps; often keep enough for 90–95%.

**Other methods**  
DBSCAN for odd-shaped clusters and outliers; t-SNE/UMAP for 2D visualisation, not for features.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Explain PCA without maths.**  
Rotate the data to look at it from the angle where it's most spread out, then drop the directions with little spread.

**Q2. Why scale data before PCA or k-means?**  
Both use distances/variance, so large-scale features would dominate.

**Q3. How do you pick k in k-means?**  
Elbow plot, silhouette score, and whether clusters make business sense.

**Q4. When would DBSCAN beat k-means?**  
Non-spherical clusters or data with noise and outliers.

---

## Part 3: Out-loud check (15 min)

> Explain PCA to a non-technical friend in 1 minute.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- K-means: assign → update → repeat
- Pick k: elbow, silhouette
- Scale before k-means/PCA
- PCA keeps directions of most variance
- DBSCAN for odd shapes + noise
