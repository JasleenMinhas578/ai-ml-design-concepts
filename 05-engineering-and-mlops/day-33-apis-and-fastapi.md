# Day 33: APIs and FastAPI

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Kth Largest Element in an Array (Heap, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** Sort and take index n−k: O(n log n).

**Best approach:** Keep a min-heap of size k; its top is the kth largest. O(n log k). Quickselect gives O(n) average.

```python
import heapq

def findKthLargest(nums, k):
    heap = []
    for n in nums:
        heapq.heappush(heap, n)
        if len(heap) > k:
            heapq.heappop(heap)
    return heap[0]
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

You expose a RAG model through `POST /ask`. Pydantic rejects requests with no question (422), the endpoint is async so it can serve many users while waiting on the LLM, and answers stream back with Server-Sent Events.

### What to understand

**REST basics**  
Resources at URLs with verbs: GET (read), POST (create), PUT/PATCH (update), DELETE.

**Status codes**  
200 OK, 201 Created, 400 bad request, 401 unauthorised, 403 forbidden, 404 not found, 422 validation error, 429 rate limited, 500 server error.

**FastAPI**  
Python web framework with type hints, automatic docs (/docs) and Pydantic validation.

**Pydantic**  
Defines request/response models and validates data automatically.

**async / await**  
Lets the server handle other requests while waiting on I/O (LLM calls, databases).

**Request lifecycle**  
Client → load balancer → server → validation → auth → business logic → response. Streaming via SSE or WebSockets.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. What happens when a request hits your API?**  
Routing, validation, authentication, logic (e.g. retrieval + LLM), and a JSON or streamed response with a status code.

**Q2. When use async in FastAPI?**  
For I/O-bound work like calling LLMs or databases.

**Q3. PUT vs PATCH?**  
PUT replaces the whole resource; PATCH updates part of it.

**Q4. 401 vs 403?**  
401 = not authenticated; 403 = authenticated but not allowed.

---

## Part 3: Out-loud check (15 min)

> Describe the life of a request through your FastAPI endpoint.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- GET/POST/PUT/PATCH/DELETE
- 2xx ok, 4xx client, 5xx server
- Pydantic validates
- async for I/O
- SSE to stream tokens
