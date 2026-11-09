# Day 34: Docker Part 1: Images and Containers

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Merge K Sorted Lists (Heap, Hard)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Collect all values, sort, rebuild: O(N log N). Or merge lists one by one: O(kN).

**Best approach:** Push each list's head into a min-heap; pop the smallest, attach it, push its next. O(N log k).

```python
import heapq

def mergeKLists(lists):
    heap = []
    for i, node in enumerate(lists):
        if node:
            heapq.heappush(heap, (node.val, i, node))
    dummy = tail = ListNode()
    while heap:
        val, i, node = heapq.heappop(heap)
        tail.next = tail = node
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))
    return dummy.next
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

Your RAG API works on your laptop but fails on the server because of a different Python version. A Dockerfile pins Python 3.11 and dependencies, so the same image runs identically everywhere.

### What to understand

**Image vs container**  
Image = read-only template (recipe). Container = a running instance of it (the meal).

**Dockerfile**  
Instructions to build an image: FROM, WORKDIR, COPY, RUN, ENV, EXPOSE, CMD.

**Layers and caching**  
Each instruction is a cached layer. Copy requirements and install first, then copy code, so code changes don't reinstall packages.

**Build and run**  
`docker build -t app .` then `docker run -p 8000:8000 app`.

**Ports, volumes, env vars**  
-p maps ports; volumes persist data outside the container; env vars hold config.

**Containers vs VMs**  
Containers share the host OS kernel: lighter and faster to start than virtual machines.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. Image vs container?**  
An image is the template; a container is a running instance.

**Q2. Why containerise an ML model?**  
Same environment everywhere, easy deployment and scaling.

**Q3. How do you speed up Docker builds?**  
Order layers from least to most frequently changing; use .dockerignore.

**Q4. Container vs VM?**  
Containers share the host kernel and are lightweight; VMs run a full OS.

---

## Part 3: Out-loud check (15 min)

> Explain image vs container and write a 6-line Dockerfile from memory.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- Image = recipe; container = running
- FROM → COPY reqs → RUN pip → COPY code → CMD
- Layer order = faster builds
- -p ports, volumes for data
- Lighter than VMs
