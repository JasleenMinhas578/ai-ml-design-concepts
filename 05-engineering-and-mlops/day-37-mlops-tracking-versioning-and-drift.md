# Day 37: MLOps: Tracking, Versioning and Drift

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Course Schedule (Topological sort, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Try every ordering: factorial time.

**Best approach:** Build a graph and in-degrees. Start with courses that have no prerequisites (BFS, Kahn's algorithm). If you can take all courses, there's no cycle.

```python
from collections import deque

def canFinish(n, prereqs):
    graph = [[] for _ in range(n)]
    indeg = [0] * n
    for a, b in prereqs:
        graph[b].append(a)
        indeg[a] += 1
    q = deque(i for i in range(n) if indeg[i] == 0)
    taken = 0
    while q:
        c = q.popleft()
        taken += 1
        for nxt in graph[c]:
            indeg[nxt] -= 1
            if indeg[nxt] == 0:
                q.append(nxt)
    return taken == n
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A food-delivery ETA model was trained before a city added bike couriers. Delivery times shift, and predictions are off by 12 minutes. Drift monitoring flags it, the team retrains on recent data, and the registry lets them roll back if needed.

### What to understand

**Experiment tracking**  
Log parameters, metrics and artefacts for every run (MLflow, Weights & Biases) so results are reproducible.

**Model registry**  
Versioned models with stages (staging, production) and easy rollback.

**Data versioning**  
Track which data trained which model (DVC, lakeFS, or dated snapshots).

**Data drift**  
Input distribution changes (new user types, new devices).

**Concept drift**  
The relationship between inputs and the label changes (what predicts fraud changes).

**Monitoring and retraining**  
Watch input stats, prediction stats and live metrics; retrain on a schedule or when drift is detected.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Data drift vs concept drift?**  
Data drift: inputs change. Concept drift: the input-to-label relationship changes.

**Q2. How do you detect drift?**  
Compare feature distributions (PSI, KS test) and monitor live performance when labels arrive.

**Q3. Why use a model registry?**  
Version control, approvals, and quick rollback.

**Q4. What makes ML reproducible?**  
Versioned code, data, config, environment and random seeds.

---

## Part 3: Out-loud check (15 min)

> Explain data vs concept drift with one example each.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Track runs: params, metrics, artefacts
- Registry: versions + rollback
- Version data too
- Data drift ≠ concept drift
- Monitor → alert → retrain
