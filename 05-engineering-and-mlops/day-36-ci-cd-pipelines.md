# Day 36: CI/CD Pipelines

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Clone Graph (Graph + hash map, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** No real brute force; the trap is infinite loops on cycles.

**Best approach:** DFS with a dict mapping original node → copy. If a node is already copied, return the copy.

```python
def cloneGraph(node):
    copies = {}
    def dfs(n):
        if n in copies:
            return copies[n]
        copy = Node(n.val)
        copies[n] = copy
        for nb in n.neighbors:
            copy.neighbors.append(dfs(nb))
        return copy
    return dfs(node) if node else None
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

A teammate pushes a change that breaks JSON parsing and production crashes. With CI/CD, the PR runs lint, unit tests and an eval suite; the failing test blocks the merge, and production stays safe.

### What to understand

**Git workflow**  
Feature branch → commits → pull request → code review → merge to main.

**Continuous integration (CI)**  
Every push/PR automatically runs lint, type checks and tests.

**Continuous delivery/deployment (CD)**  
After CI passes, build the Docker image, push to registry and deploy, first to staging, then production.

**GitHub Actions**  
YAML workflows in `.github/workflows/` triggered on push or PR.

**Testing**  
Unit tests (pytest) for functions, integration tests for services, eval tests for LLM quality.

**Safe releases**  
Staging environment, canary or blue-green deployments, and fast rollback.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Walk me through a CI/CD pipeline.**  
PR → lint → tests → build image → push → deploy to staging → checks → deploy to production with rollback ready.

**Q2. CI vs CD?**  
CI checks every change automatically; CD automatically ships changes that pass.

**Q3. What would you test in a RAG app?**  
Chunking logic, retrieval on known queries, prompt formatting, JSON parsing, and an eval set.

**Q4. What is a canary deployment?**  
Release to a small percentage of users first, watch metrics, then roll out fully.

---

## Part 3: Out-loud check (15 min)

> Draw a CI/CD pipeline from PR to production.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Branch → PR → review → merge
- CI: lint + test on every push
- CD: build → staging → prod
- GitHub Actions YAML
- Canary + rollback
