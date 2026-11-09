# Day 35: Docker Part 2: Production Images and Compose

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Number of Islands (Graph DFS/BFS, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** None really slower; the common mistake is not marking cells as visited.

**Best approach:** Scan the grid; on each '1', count an island and flood-fill (DFS/BFS) to mark the whole island visited. O(rows × cols).

```python
def numIslands(grid):
    rows, cols = len(grid), len(grid[0])
    def dfs(r, c):
        if r < 0 or c < 0 or r >= rows or c >= cols or grid[r][c] != '1':
            return
        grid[r][c] = '0'
        dfs(r+1, c); dfs(r-1, c); dfs(r, c+1); dfs(r, c-1)
    count = 0
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                count += 1
                dfs(r, c)
    return count
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Your image is 3 GB because it includes compilers and test files. A multi-stage build brings it to 400 MB. docker-compose starts the API, Postgres with pgvector and Redis together with one command.

### What to understand

**Multi-stage builds**  
Build in one stage, copy only the final artefacts into a slim runtime stage.

**Slim base images**  
python:3.11-slim instead of full images; fewer packages, smaller attack surface.

**docker-compose**  
Define multiple services (api, db, cache) in YAML and run them together.

**Registries**  
Store and share images: Docker Hub, AWS ECR, GitHub Container Registry. Tag with versions, not just 'latest'.

**Secrets**  
Never bake API keys into images; pass them at runtime via env vars or a secrets manager.

**Health checks and non-root**  
Add HEALTHCHECK and run as a non-root user for safety.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Why multi-stage builds?**  
Smaller, safer images without build tools.

**Q2. Why use docker-compose?**  
To run and connect several services locally with one config.

**Q3. How do you handle API keys in Docker?**  
Inject at runtime via env vars or a secrets manager, never in the image.

**Q4. Why avoid the 'latest' tag in production?**  
It's ambiguous; version tags make deployments reproducible and rollbacks easy.

---

## Part 3: Out-loud check (15 min)

> Explain why compose, multi-stage builds and runtime secrets matter.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Multi-stage = small image
- Slim base, non-root user
- Compose = multi-service local
- Push to registry with version tags
- Secrets at runtime only
